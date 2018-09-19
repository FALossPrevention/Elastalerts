# Elastalerts
Creation of Elastalerts for FA Loss Prevention
Creation of email alerts when specific fraud patterns are detected by our Kibana Fraud Dashboard.
es_host: holog02.mecnet.lcl
es_port: 9200
index: logstash-*
name: Sales Audit: GoPro HERO6 Black
type: frequency
num_events: 1
timeframe:
  hours: 1
filter:
- query:
   query_string:
     query: "\"610163\" AND \"order_tot\" AND \"new_mbr\" AND \"sh_name\" AND \"sh_city\" AND \"sh_email\" AND \"bl_name\" AND \"bl_city\""
# The alert is used when a match is found
alert:
- email
alert_subject: "Sales Audit: GoPro HERO6 Black Detected"
realert:
  minutes: 0
include: ["@timestamp", "logLevel", "message", "host"]
use_local_time: true
email:
- fa_lprep@mec.ca
