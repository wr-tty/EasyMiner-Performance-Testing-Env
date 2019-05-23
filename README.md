# EasyMiner Performance testing Environment

Performance testing environment for [EasyMiner](https://github.com/KIZI/EasyMiner) project. Using docker-compose.yaml to setup performance testing. Contains Grafana, Prometheus, Node exporter, cAdvisor and Taurus.

## Prerequisites

* Docker

## Installing

* create project root directory
* clone [EasyMiner-Performance-Testing-Env](https://github.com/wr-tty/EasyMiner-Performance-Testing-Env) project into created directory
* clone [EasyMiner-Performance-Tests](https://github.com/wr-tty/EasyMiner-Performance-Tests) project into same created directory
    * structure should look like this
        ~~~
        project_root_directory
        ├── EasyMiner-Performance-Testing-Env
        └── EasyMiner-Performance-Tests
        ~~~
* set folders grafana_data and prometheus_data in EasyMiner-Performance-Testing-Env folder to permission mode 777
    * should be writeable for group and others
* run command
    ~~~
    docker-compose up -d
    ~~~
    
## Troubleshooting

### Grafana
    
Login form display error after send with right credentials:

* Solution 1:
    * Check grafana.db file permission mode (should be writable for "others")
* Solution 2:
    1. Turn off login in docker-compose.xml file. 
        * Comment uncommented lines with variables:
            * GF_AUTH_BASIC_ENABLED
            * GF_SECURITY_ADMIN_PASSWORD
            * GF_SECURITY_ADMIN_USER
    2. Turn on anonymous user
        * Uncomment lines with variables: 
            * GF_AUTH_BASIC_ENABLED
            * GF_AUTH_DISABLE_LOGIN_FORM
            * GF_AUTH_ANONYMOUS_ENABLED
            * GF_USER_AUTO_ASSIGN_ORG_ROLE

