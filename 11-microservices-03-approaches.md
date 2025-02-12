# Домашнее задание к занятию «Микросервисы: подходы»

Вы работаете в крупной компании, которая строит систему на основе микросервисной архитектуры.
Вам как DevOps-специалисту необходимо выдвинуть предложение по организации инфраструктуры для разработки и эксплуатации.


## Задача 1: Обеспечить разработку

Предложите решение для обеспечения процесса разработки: хранение исходного кода, непрерывная интеграция и непрерывная поставка. 
Решение может состоять из одного или нескольких программных продуктов и должно описывать способы и принципы их взаимодействия.

Решение должно соответствовать следующим требованиям:
- облачная система;
- система контроля версий Git;
- репозиторий на каждый сервис;
- запуск сборки по событию из системы контроля версий;
- запуск сборки по кнопке с указанием параметров;
- возможность привязать настройки к каждой сборке;
- возможность создания шаблонов для различных конфигураций сборок;
- возможность безопасного хранения секретных данных (пароли, ключи доступа);
- несколько конфигураций для сборки из одного репозитория;
- кастомные шаги при сборке;
- собственные докер-образы для сборки проектов;
- возможность развернуть агентов сборки на собственных серверах;
- возможность параллельного запуска нескольких сборок;
- возможность параллельного запуска тестов.

Обоснуйте свой выбор.

---     
Хорошим вариантом было бы использование **GitHub Actions (или GitLab CI/CD) с Docker и HashiCorp Vault.**         

Почему:
1. Все предложенные инструменты являются облачными, что обеспечивает доступность и масштабируемость.          
2. GitHub и GitLab предлагают встроенные CI/CD функции, что упрощает настройку и управление процессами.           
3. Docker и HashiCorp Vault обеспечивают возможность кастомизации и безопасного управления секретами.          
4. Поддержка параллельных сборок и тестов позволяет оптимизировать время разработки.          

Принципы взаимодействия тут следующие:          
Хранение кода: Исходный код хранится в репозиториях **GitHub или GitLab**, что позволяет разработчикам работать совместно и управлять версиями.             
Сборка и тестирование: **GitHub Actions или GitLab CI/CD** отслеживают изменения в репозитории и автоматически запускают сборки и тесты по событиям (например, push или pull request). Также можно запускать сборки вручную с указанием параметров.           
Управление секретами: **HashiCorp Vault** используется для безопасного хранения секретов, которые могут быть переданы в CI/CD процессы при необходимости.        
Контейнеризация: **Docker** используется для создания и развертывания приложений в контейнерах, что обеспечивает консистентность среды выполнения.           
Параллельные сборки: **GitHub Actions или GitLab CI/CD** позволяют запускать несколько сборок и тестов параллельно, что ускоряет процесс разработки.             

Возможности GitHub Actions (или GitLab CI/CD):     
- Запуск сборки по событию из системы контроля версий (например, push, pull request).       
- Запуск сборки по кнопке с указанием параметров через интерфейс.          
- Привязка настроек к каждой сборке через переменные окружения и секреты.         
- Поддержка кастомных шагов при сборке, что позволяет добавлять специфические команды и скрипты.        
- Создание собственных Docker-образов для сборки проектов.        
- Поддержка параллельного запуска нескольких сборок и тестов.

Возможности Docker:          
- Создание собственных Docker-образов для изоляции среды сборки.       
- Хранение образов в Docker Hub или в частных реестрах (например, GitHub Container Registry).

Возможности HashiCorp Vault:     
- Интеграция с CI/CD системами для безопасного доступа к секретам во время сборки и развертывания.
- Поддержка различных методов аутентификации и шифрования.

Что касается выбора между GitHub или GitLab:       
**Плюсы GitHub:**            
- Сообщество и экосистема: GitHub имеет более обширное сообщество, что означает больше доступных ресурсов, библиотек и интеграций.       
- Простота использования: Многие пользователи находят интерфейс GitHub более интуитивно понятным и удобным.             
- Marketplace: GitHub Actions предоставляет мощный и гибкий механизм для автоматизации процессов CI/CD, позволяя пользователям создавать сложные рабочие процессы с помощью простого синтаксиса YAML. Хотя GitLab также предлагает CI/CD, GitHub Actions интегрируется более глубоко в экосистему GitHub и имеет обширный Marketplace с готовыми действиями. Он предлагает множество сторонних приложений и интеграций, которые можно легко добавить к проектам. Хотя GitLab также имеет свои интеграции, Marketplace GitHub более развит и разнообразен.            
- Открытые проекты: GitHub стал домом для множества известных проектов с открытым исходным кодом и имеет более крупное сообщество разработчиков. Это создает более широкие возможности для сотрудничества и обмена знаниями.         

**Плюсы GitLab:**     
- Все в одном: GitLab предлагает интегрированные функции для управления проектами, CI/CD, мониторинга и безопасного управления кодом в одном инструменте. Это может быть удобным для команд, которые предпочитают единую платформу.           
- Более мощный CI/CD: GitLab CI/CD считается более гибким и мощным, позволяя более детальную настройку пайплайнов и использование различных методов развертывания.         
- Бесплатные функции: GitLab предлагает больше функционала в бесплатной версии, включая неограниченные приватные репозитории и более гибкие возможности для CI/CD.        
- Self-hosting: GitLab предлагает более удобные решения для самохостинга, что может быть критически важным для некоторых организаций.  
        
Если команда уже использует GitLab или если нужны его специфические функции, такие как более мощный CI/CD или всеобъемлющая платформа для управления проектами, GitLab может быть отличным выбором.         

---

## Задача 2: Логи

Предложите решение для обеспечения сбора и анализа логов сервисов в микросервисной архитектуре.
Решение может состоять из одного или нескольких программных продуктов и должно описывать способы и принципы их взаимодействия.

Решение должно соответствовать следующим требованиям:
- сбор логов в центральное хранилище со всех хостов, обслуживающих систему;
- минимальные требования к приложениям, сбор логов из stdout;
- гарантированная доставка логов до центрального хранилища;
- обеспечение поиска и фильтрации по записям логов;
- обеспечение пользовательского интерфейса с возможностью предоставления доступа разработчикам для поиска по записям логов;
- возможность дать ссылку на сохранённый поиск по записям логов.

Обоснуйте свой выбор.

---
Предлагаю использовать систему, состоящую из следующих компонентов:      

**1. Fluent Bit / Fluentd / Filebeat (Сбор логов)**         
Эти инструменты предназначены для сбора, обработки и передачи логов. Fluent Bit является легковесной версией, оптимизированной для высоких нагрузок, и может использоваться для сбора логов из stdout контейнеров. Fluent Bit будет запущен на каждом хосте, где работают микросервисы. Он будет собирать логи из stdout и отправлять их в центральное хранилище (например, Elasticsearch).        
**2. Elasticsearch (Центральное хранилище)**         
Это распределенная поисковая и аналитическая система, которая позволяет хранить и индексировать логи для последующего поиска и анализа. Fluent Bit будет отправлять собранные логи в Elasticsearch, где они будут индексироваться для быстрого поиска и фильтрации.         
**3. Kibana (Пользовательский интерфейс)**       
Это веб-интерфейс, который предоставляет возможность визуализации и анализа данных, хранящихся в Elasticsearch. Он позволяет пользователям выполнять поиск, фильтрацию и визуализацию логов. Kibana будет подключаться к Elasticsearch и предоставлять интерфейс для разработчиков, позволяя им искать и фильтровать логи. Также Kibana поддерживает создание дашбордов и сохранение поисковых запросов, что соответствует требованиям.       
**4. Logstash (необязательно) (Доп обработка)**       
Logstash может использоваться для более сложной обработки логов, если это необходимо. Он может выполнять фильтрацию, преобразование и обогащение данных перед отправкой их в Elasticsearch. Если требуется дополнительная обработка, Fluent Bit может отправлять логи в Logstash, а затем Logstash будет отправлять их в Elasticsearch.         

Преимущества этих компонентов:
- Минимальные требования к приложениям: Fluent Bit может собирать логи напрямую из stdout, что минимизирует изменения в коде микросервисов.      
- Гарантированная доставка: Fluent Bit поддерживает механизмы повторной отправки, что обеспечивает надежную доставку логов в Elasticsearch.     
- Поиск и фильтрация: Elasticsearch предоставляет мощные возможности для поиска и фильтрации, что позволяет разработчикам эффективно анализировать логи.     
- Пользовательский интерфейс: Kibana предлагает удобный интерфейс для работы с логами, что соответствует требованиям доступа разработчиков.    
- Гибкость: Решение легко масштабируемо и может быть адаптировано под разные требования и нагрузки.     

Что касается выбора между Filebeat и Fluent Bit:    

Преимущества Filebeat:     
- Интеграция с ELK Stack: Filebeat является частью Elastic Stack (ELK), что обеспечивает более тесную интеграцию с Elasticsearch и Kibana. Это упрощает настройку и управление.    
- Поддержка различных форматов: Filebeat поддерживает множество форматов логов и может легко обрабатывать различные типы данных, включая JSON, лог-файлы и другие.      
- Модули для упрощения настройки: Filebeat предлагает модули, которые предоставляют преднастроенные конфигурации для сбора и обработки логов из популярных приложений (например, Nginx, Apache, MySQL и др.). Это может значительно упростить процесс настройки.    
- Обработка на уровне хоста: Filebeat может работать на уровне хоста, собирая логи из файловой системы, что может быть полезно, если ваши приложения записывают логи в файлы, а не в stdout.      
- Меньшая нагрузка на ресурсы: Filebeat имеет низкие требования к ресурсам и может быть оптимизирован для работы в условиях ограниченных ресурсов.

Преимущества Fluent Bit:     
- Легковесность и производительность: Fluent Bit более легковесен и оптимизирован для работы в средах с высокими нагрузками, таких как Kubernetes и Docker. Он может быть более эффективным в сценариях с большим объемом логов.      
- Гибкость в обработке: Fluent Bit предоставляет мощные возможности для фильтрации и обработки данных на лету, что может быть полезно для более сложных сценариев обработки логов.    
- Поддержка различных источников: Fluent Bit может собирать логи не только из файлов, но и из различных источников, таких как системные журналы, stdout контейнеров и другие.     
- Настройка и конфигурация: Fluent Bit имеет простую и понятную конфигурацию, что делает его удобным для быстрого развертывания и настройки.      

Такии образом, если система уже использует Elastic Stack и нужны модули для упрощения настройки и простота интеграции, Filebeat может быть предпочтительным выбором. Fluent Bit может оказаться более подходящим, если проект требует высокой производительности и легковесности в условиях микросервисной архитектуры.

---


## Задача 3: Мониторинг

Предложите решение для обеспечения сбора и анализа состояния хостов и сервисов в микросервисной архитектуре.
Решение может состоять из одного или нескольких программных продуктов и должно описывать способы и принципы их взаимодействия.

Решение должно соответствовать следующим требованиям:
- сбор метрик со всех хостов, обслуживающих систему;
- сбор метрик состояния ресурсов хостов: CPU, RAM, HDD, Network;
- сбор метрик потребляемых ресурсов для каждого сервиса: CPU, RAM, HDD, Network;
- сбор метрик, специфичных для каждого сервиса;
- пользовательский интерфейс с возможностью делать запросы и агрегировать информацию;
- пользовательский интерфейс с возможностью настраивать различные панели для отслеживания состояния системы.

Обоснуйте свой выбор.

---
С этой задачей хорошо справится система, состоящая из следующих компонентов:       
**Prometheus** — для сбора и хранения метрик. Широко используется в микросервисной архитектуре и отлично подходит для сбора метрик из распределенных систем.
Поддерживает мощный язык запросов (PromQL), который позволяет выполнять сложные запросы и агрегировать данные.     
**Grafana** — для визуализации метрик и создания пользовательских панелей. Обеспечивает гибкий и интуитивно понятный интерфейс для визуализации метрик и создания дашбордов.
Позволяет настраивать уведомления и оповещения на основе собранных метрик.         
**Node Exporter** — для сбора метрик состояния ресурсов хостов (CPU, RAM, HDD, Network) и **cAdvisor** — для сбора метрик потребляемых ресурсов для контейнеров и сервисов (CPU, RAM, HDD, Network). Эти инструменты обеспечивают сбор метрик состояния хостов и контейнеров, что позволяет получить полное представление о производительности системы.
Легкость в установке и настройке. 

**1. Сбор метрик:**      
Node Exporter устанавливается на каждом хосте и собирает метрики состояния ресурсов (CPU, RAM, HDD, Network). Он экспонирует эти метрики в формате, понятном Prometheus.
cAdvisor запускается в контейнерах и собирает метрики для каждого сервиса, работающего в контейнерах (например, Docker). Он также экспонирует метрики в формате Prometheus.
p.s. - Custom Exporters могут быть разработаны для сбора специфичных метрик для определенных сервисов (например, метрики производительности веб-приложений, API и т.д.). Эти экспортёры также должны быть совместимы с форматом Prometheus.         

**2.Хранение метрик:**    
Prometheus периодически опрашивает **Node Exporter, cAdvisor** и другие экспортёры для сбора метрик. Он хранит эти метрики в своей базе данных временных рядов, что позволяет эффективно выполнять запросы и агрегировать данные.       

**3.Визуализация метрик:**     
Grafana интегрируется с Prometheus как источник данных и предоставляет мощный интерфейс для визуализации метрик. Пользователи могут создавать настраиваемые панели, выбирать метрики для отображения и настраивать различные визуализации (графики, таблицы и т.д.), создавать дашбордов, которые могут отображать состояние системы в реальном времени и предоставлять аналитическую информацию по собранным метрикам.        

Почему Prometheus и Grafana могут быть предпочтительнее Zabbix?        
- Масштабируемость: Prometheus лучше подходит для распределенных систем и микросервисов, особенно в облачных средах. Он может легко масштабироваться и обрабатывать большие объемы метрик.       
- Запросы и агрегация: Prometheus использует язык запросов PromQL, который предоставляет мощные возможности для агрегации и анализа данных.        
- Гибкость в визуализации: Grafana предлагает более богатый и гибкий интерфейс для визуализации данных, позволяя пользователям создавать настраиваемые дашборды.      
- Культурная совместимость: В сообществе DevOps и облачных технологий Prometheus и Grafana стали стандартом для мониторинга микросервисов, что может облегчить интеграцию и поддержку.  

Преимущества Zabbix перед комбинацией Grafana + Prometheus:      
**1. Комплексное решение "всё в одном":**
Zabbix: Это полноценная система мониторинга, которая объединяет сбор, хранение, обработку и визуализацию данных в одном инструменте. В Zabbix нет необходимости интегрировать несколько компонентов, как в случае с Prometheus и Grafana.       
**2. Встроенные функции оповещения и триггеры:**
Zabbix: Предоставляет мощные и гибкие возможности для настройки триггеров и оповещений. Пользователи могут настраивать сложные условия для уведомлений, а также использовать различные каналы (e-mail, SMS, Jabber и т.д.) для оповещения.        
Prometheus + Grafana: Хотя Prometheus также поддерживает оповещения через Alertmanager, настройка может быть менее интуитивной и требует дополнительной конфигурации.        
**3. Поддержка различных протоколов для сбора данных:**
Zabbix: Поддерживает множество протоколов для сбора данных, включая SNMP, IPMI, JMX, а также может работать с агентами, которые могут собирать метрики с различных систем.        
Prometheus: Хотя Prometheus поддерживает различные способы сбора данных (например, через HTTP и экспортеры), он не имеет встроенной поддержки ряда протоколов, таких как SNMP, без дополнительных инструментов.       
**4. Мониторинг состояния и производительности на уровне хостов:**
Zabbix: Позволяет отслеживать не только метрики, но и состояние оборудования, включая состояние дисков, сетевых интерфейсов и т.д., с помощью встроенных инструментов.        
Prometheus: Основной акцент делается на метрики приложений и сервисов, и для мониторинга состояния хостов могут потребоваться дополнительные экспортёры (например, Node Exporter).         
**5. Управление конфигурацией через веб-интерфейс:**          
Zabbix: Предоставляет удобный веб-интерфейс для управления конфигурацией, создания хостов, настройки триггеров и оповещений, что может быть более интуитивным для пользователей.         
Prometheus + Grafana: Настройка и конфигурация Prometheus часто требуют редактирования конфигурационных файлов, что может быть менее удобно для некоторых пользователей.          
**6. Встроенные функции отчетности:**      
Zabbix: Имеет встроенные инструменты для создания отчетов, которые позволяют пользователям легко генерировать и экспортировать отчеты о состоянии системы и производительности.       
Grafana: Хотя Grafana предоставляет возможности визуализации, создание отчетов требует дополнительных настроек и может не быть столь простым, как в Zabbix.        
**7. Исторические данные и хранение:**        
Zabbix: Способен хранить данные в своей базе данных, что позволяет легко управлять историческими данными и выполнять долгосрочный анализ.       
Prometheus: Хранение данных осуществляется в формате временных рядов, и хотя это эффективно, он может не поддерживать такие же возможности для долгосрочного хранения и анализа, как Zabbix без дополнительных решений.     

Таким образом, если требуется комплексное решение с простотой в использовании и мощными функциями оповещения, Zabbix может быть отличным выбором. Если же акцент делается на гибкости, масштабируемости и возможностях анализа данных, то Prometheus и Grafana могут предоставить лучшие результаты.

---

## Задача 4: Логи * (необязательная)

Продолжить работу по задаче API Gateway: сервисы, используемые в задаче, пишут логи в stdout. 

Добавить в систему сервисы для сбора логов Vector + ElasticSearch + Kibana со всех сервисов, обеспечивающих работу API.

### Результат выполнения: 

docker compose файл, запустив который можно перейти по адресу http://localhost:8081, по которому доступна Kibana.
Логин в Kibana должен быть admin, пароль qwerty123456.


## Задача 5: Мониторинг * (необязательная)

Продолжить работу по задаче API Gateway: сервисы, используемые в задаче, предоставляют набор метрик в формате prometheus:

- сервис security по адресу /metrics,
- сервис uploader по адресу /metrics,
- сервис storage (minio) по адресу /minio/v2/metrics/cluster.

Добавить в систему сервисы для сбора метрик (Prometheus и Grafana) со всех сервисов, обеспечивающих работу API.
Построить в Graphana dashboard, показывающий распределение запросов по сервисам.

### Результат выполнения: 

docker compose файл, запустив который можно перейти по адресу http://localhost:8081, по которому доступна Grafana с настроенным Dashboard.
Логин в Grafana должен быть admin, пароль qwerty123456.

---

### Как оформить ДЗ?

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---
