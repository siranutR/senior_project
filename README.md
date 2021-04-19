# senior_project
sudo apt-get install logstash
sudo apt-get install elasticsearch
sudo apt-get install kibana
sudo apt-get install metricbeat

Open Kibana config file at: /etc/kibana/kibana.yml, and make sure you have the following configurations defined:
server.port: 5601 elasticsearch.url: "http://localhost:9200"

Next, create a new Logstash configuration file at: /etc/logstash/conf.d/configname-01.conf:

Enter the following Logstash configuration (change the path to the your log accordingly):

input { file { path => "log_path.log" 
start_position => "beginning" sincedb_path => "/dev/null" } } 

filter { grok { match => { "message" => "%{COMBINEDAPACHELOG}" } } 
date { match => [ "timestamp" , "dd/MMM/yyyy:HH:mm:ss Z" ] } 
geoip { source => "clientip" } } 
output { elasticsearch { hosts => ["localhost:9200"] } }

Or





input {
  beats {
    port => 5044
  }
}

output {
  elasticsearch {
    hosts => ["http://localhost:9200"]
  }
}


If you all set up
Start service of ELK stack
Then open kibana website
In Kibana, go to Management → Kibana Index Patterns. Kibana should display the Logstash index And create index pattern
Then you should be able to config visualization in kibana





