rackspace-monitoring-varnish
============================

Rackspace Cloud Monitoring agent plugin for Varnish

# Installation

## Step 1: Place varnish.sh into /usr/lib/rackspace-monitoring-agent/plugins/ on each Varnish server. 
## Step 2: Create a Cloud Monitoring Check of type "agent.plugin". Also specify the following values in the details argument:

| Check Attribute | Value                             | Description                                       |
|:-------------- |:-----------------------------------|:------------------------------------------------- |
| file           | varnish.sh                         | The file name of the plugin script                |
| args           | cache_hit,cache_hitpass,cache_miss | Comma-separated list of valid varnishstat metrics |  

## Step 3: Start recieving metrics for:

| Metric Name      | Type         | Description                                                           |
|:---------------- |:------------ |:--------------------------------------------------------------------- |
| hit_percent      | float        | 100 - (cache_miss/cache_hit)                                          |
| healthy_backends | int32        | Number of backends reporting healthy from `varnishadm debug.health`   |
| args (above)     | gauge        | Current value of each varnishstat metric passed in                    |

## Step 4: Create a Cloud Monitoring Alarm that alarms on:

```if (metric['healthy_backends'] < 1) {
	return new AlarmStatus(CRITICAL, 'Varnish doesnt have any backends!');
}

if (metric['healthy_backends'] < 2) {
	return new AlarmStatus(WARNING, 'Varnish only has #{healthy_backends} healthy backend.');
}

return new AlarmStatus(OK, 'Varnish has \#{healthy_backends} backends.');```