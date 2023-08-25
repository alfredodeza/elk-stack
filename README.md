# ELK Stack
A sample all-in-one ELK stack repo with instructions for running in a single machine. Find out how to properly configure and install everything you need to have the ELK stack running in your environment. 

The ELK stack for this reference architecture is comprised of the following components:

1. Elasticsearch
2. Logstash
3. Kibana
4. Filebeat

## Install

These installation instructions follows the documentation for Debian based systems. Refer to the [documentation on installation](https://www.elastic.co/guide/en/elastic-stack/current/installing-elastic-stack.html) for other systems.

1. Setup keys and dependencies with the APT package manager:
    
    ```bash
    wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo gpg --dearmor -o /usr/share/keyrings/elasticsearch-keyring.gpg
    ```
    
    Ensure that the `apt-transport-https` package is installed on the system:
    
    ```bash
    sudo apt-get install apt-transport-https
    ```

    Save the repository definition to `/etc/apt/sources.list.d/elastic-8.x.list`:
    
    ```bash
    echo "deb [signed-by=/usr/share/keyrings/elasticsearch-keyring.gpg] https://artifacts.elastic.co/packages/8.x/apt stable main" | sudo tee /etc/apt/sources.list.d/elastic-8.x.list
    ```

2. Install the Elasticsearch Debian package:
    
    ```bash
    sudo apt-get update && sudo apt-get install elasticsearch
    ```

    This will generate a token that you need to save:

    ```
    The generated password for the elastic built-in superuser is : NNNNNNNNNNNNN
    ```

3. Install Kibana:
        
    ```bash
    sudo apt-get install kibana
    ```
4. Install Logstash:
        
    ```bash
    sudo apt-get install logstash
    ```

5. Install Filebeat:
        
    ```bash
    sudo apt-get install filebeat
    ```

6. Enable and start all the services:

    ```bash
    sudo /bin/systemctl daemon-reload
    sudo /bin/systemctl enable elasticsearch.service
    sudo systemctl enable filebeat
    sudo systemctl start logstash.service
    sudo /bin/systemctl daemon-reload
    sudo /bin/systemctl enable kibana.service
    ```
    
    Include the Elasticsearch service:

    ```bash
    ### NOT starting on installation, please execute the following statements to configure elasticsearch service to start automatically using systemd
    sudo systemctl daemon-reload
    sudo systemctl enable elasticsearch.service
    ### You can start elasticsearch service by executing
    sudo systemctl start elasticsearch.service
    ```