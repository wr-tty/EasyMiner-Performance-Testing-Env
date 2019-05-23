# EasyMiner Performance Testing Environment

Performance testing environment for [EasyMiner](https://github.com/KIZI/EasyMiner) project. Using docker-compose.yaml to setup performance testing. Contains Grafana, Prometheus, Node exporter, cAdvisor and Taurus.

## Prerequisites

* Docker

## Installing

* clone repository and his submodules with command:
    ~~~bash
    git clone --recurse-submodules git@github.com:wr-tty/EasyMiner-Performance-Testing-Env.git
    ~~~
* Set folders grafana_data and prometheus_data in EasyMiner-Performance-Testing-Env folder to permission mode 777.
    * Should be writeable for group and others.
    * You can run command:
        ~~~bash
        chmod go+w EasyMiner-Performance-Testing-Env/grafana_data/ EasyMiner-Performance-Testing-Env/prometheus_data/
        ~~~
* Set file EasyMiner-Performance-Testing-Env/grafana_data/grafana.db file to permission mode 777.
    * Should be writeable for group and others.
    * You can run command:
        ~~~bash
        chmod go+w EasyMiner-Performance-Testing-Env/grafana_data/grafana.db
        ~~~
* Run EasyMiner application with:
    ~~~bash
    docker-compose -f docker-compose-app.yaml up -d
    ~~~
* Run monitoring with:
    ~~~bash
    docker-compose -f docker-compose-monitoring.yaml up -d
    ~~~
* Run Taurus tests with:
    ~~~bash
    docker-compose -f docker-compose-performance-testing.yaml up -d
    ~~~

## Features

* Pass dataset path by selection to TAURUS_TEST_DATASET variable in docker-compose-performance-testing.yaml.
    * Escape special characters with backslash character "\" 
    * TAURUS_TEST_DATASET variable accepts file path from testing-data folder.
    
## Troubleshooting

### Grafana

**Taurus test result section in Grafana doesn't showing up test results.**

* Check your firewall. You should allow ports mentioned in docker-compose.yaml. Allow ports:
    * 9090 (Prometheus)
    * 9000 (cAdvisor)
    * 9100 (Node-exporter)
    * 8008 (Taurus prometheus exporter)

**Login form display error after send with right credentials.**

* Solution 1:
    * Check grafana.db file permission mode (should be writable for "others").
* Solution 2:
    1. Turn off login in docker-compose.xml file. 
        * Comment uncommented lines with variables:
            * GF_AUTH_BASIC_ENABLED
            * GF_SECURITY_ADMIN_PASSWORD
            * GF_SECURITY_ADMIN_USER
    2. Turn on anonymous user.
        * Uncomment lines with variables: 
            * GF_AUTH_BASIC_ENABLED
            * GF_AUTH_DISABLE_LOGIN_FORM
            * GF_AUTH_ANONYMOUS_ENABLED
            * GF_USER_AUTO_ASSIGN_ORG_ROLE

