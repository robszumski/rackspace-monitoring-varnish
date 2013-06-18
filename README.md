rackspace-monitoring-varnish
============================

Rackspace Cloud Monitoring agent plugin for Varnish

# Installation

1. Place varnish.sh into /usr/lib/rackspace-monitoring-agent/plugins/ on each Varnish server. 
2. Create a Cloud Monitoring Check of type "agent.plugin". Also specify the following values:

| Check Attribute | Value                             | Description                                       |
|:-------------- |:-----------------------------------|:------------------------------------------------- |
| file           | varnish.sh                         | The file name of the plugin script                |
| args           | cache_hit,cache_hitpass,cache_miss | Comma-separated list of valid varnishstat metrics |
| timeout        | 29                                 | Timeout value                                     |    

3. Create a Cloud Monitoring Alarm that specifies how to alarm you:

INSERT EXAMPLE