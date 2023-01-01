# ST2 Hello Pack


## Install
```
root@7afd86a716c4:/opt/stackstorm/packs.dev/hello_st2# st2 pack install file:///opt/stackstorm/packs.dev/hello_st2

        [ succeeded ] init_task
        [ succeeded ] download_pack
        [ succeeded ] make_a_prerun
        [ succeeded ] get_pack_dependencies
        [ succeeded ] check_dependency_and_conflict_list
        [ succeeded ] install_pack_requirements
        [ succeeded ] get_pack_warnings
        [ succeeded ] register_pack

+-------------+--------------------------------------------------------------+
| Property    | Value                                                        |
+-------------+--------------------------------------------------------------+
| ref         | hello_st2                                                    |
| name        | Hello StackStorm                                             |
| description | Simple pack containing examples of sensor, rule, and action. |
| version     | 0.1.0                                                        |
| author      | StackStorm, Inc.                                             |
+-------------+--------------------------------------------------------------+
```


## Action
```
root@7afd86a716c4:/opt/stackstorm/packs.dev/hello_st2# st2 action list -p hello_st2
+-----------------+-----------+-------------------+
| ref             | pack      | description       |
+-----------------+-----------+-------------------+
| hello_st2.greet | hello_st2 | Greet StackStorm! |
+-----------------+-----------+-------------------+

root@7afd86a716c4:/opt/stackstorm/packs.dev/hello_st2# st2 action get hello_st2.greet
+---------------+--------------------------------------------------------------+
| Property      | Value                                                        |
+---------------+--------------------------------------------------------------+
| id            | 63b0c0e526171b55c61d7cf9                                     |
| uid           | action:hello_st2:greet                                       |
| ref           | hello_st2.greet                                              |
| pack          | hello_st2                                                    |
| name          | greet                                                        |
| description   | Greet StackStorm!                                            |
| enabled       | True                                                         |
| entry_point   | greet.sh                                                     |
| runner_type   | local-shell-script                                           |
| parameters    | {                                                            |
|               |     "greeting": {                                            |
|               |         "type": "string",                                    |
|               |         "description": "Greeting you want to say to          |
|               | StackStorm (i.e. Hello, Hi, Yo, etc.)",                      |
|               |         "required": true,                                    |
|               |         "position": 1                                        |
|               |     }                                                        |
|               | }                                                            |
| metadata_file | actions/greet.yaml                                           |
| notify        |                                                              |
| output_schema |                                                              |
| tags          |                                                              |
+---------------+--------------------------------------------------------------+

root@7afd86a716c4:/opt/stackstorm/packs.dev/hello_st2# st2 run hello_st2.greet greeting=Hi
.
id: 63b14beb26171b55c61d7d09
action.ref: hello_st2.greet
context.user: st2admin
parameters: 
  greeting: Hi
status: succeeded
start_timestamp: Sun, 01 Jan 2023 09:01:31 UTC
end_timestamp: Sun, 01 Jan 2023 09:01:31 UTC
result: 
  failed: false
  return_code: 0
  stderr: ''
  stdout: Hi, StackStorm!
  succeeded: true

root@7afd86a716c4:/opt/stackstorm/packs.dev/hello_st2# st2 execution list -n 3
+--------------------------+-----------------+--------------+------------------------+-------------------+---------------+
| id                       | action.ref      | context.user | status                 | start_timestamp   | end_timestamp |
+--------------------------+-----------------+--------------+------------------------+-------------------+---------------+
| 63b14bb66709baa4f995a28a | hello_st2.greet | stanley      | succeeded (0s elapsed) | Sun, 01 Jan 2023  | Sun, 01 Jan   |
|                          |                 |              |                        | 09:00:38 UTC      | 2023 09:00:38 |
|                          |                 |              |                        |                   | UTC           |
| 63b14beb26171b55c61d7d09 | hello_st2.greet | st2admin     | succeeded (0s elapsed) | Sun, 01 Jan 2023  | Sun, 01 Jan   |
|                          |                 |              |                        | 09:01:31 UTC      | 2023 09:01:31 |
|                          |                 |              |                        |                   | UTC           |
| 63b14bf26709baa4f995a295 | hello_st2.greet | stanley      | succeeded (0s elapsed) | Sun, 01 Jan 2023  | Sun, 01 Jan   |
|                          |                 |              |                        | 09:01:38 UTC      | 2023 09:01:38 |
|                          |                 |              |                        |                   | UTC           |
+--------------------------+-----------------+--------------+------------------------+-------------------+---------------+
+------------------------------------------------------------------------------------------------------------------------+
| Note: Only first 3 action executions are displayed. Use -n/--last flag for more results.                               |
+------------------------------------------------------------------------------------------------------------------------+

root@7afd86a716c4:/opt/stackstorm/packs.dev/hello_st2# st2 execution get 63b14beb26171b55c61d7d09
id: 63b14beb26171b55c61d7d09
action.ref: hello_st2.greet
context.user: st2admin
parameters: 
  greeting: Hi
status: succeeded (0s elapsed)
start_timestamp: Sun, 01 Jan 2023 09:01:31 UTC
end_timestamp: Sun, 01 Jan 2023 09:01:31 UTC
log: 
  - status: requested
    timestamp: '2023-01-01T09:01:31.253000Z'
  - status: scheduled
    timestamp: '2023-01-01T09:01:31.369000Z'
  - status: running
    timestamp: '2023-01-01T09:01:31.384000Z'
  - status: succeeded
    timestamp: '2023-01-01T09:01:31.425000Z'
result: 
  failed: false
  return_code: 0
  stderr: ''
  stdout: Hi, StackStorm!
  succeeded: true
```
  
  
## Rule
```
root@7afd86a716c4:/opt/stackstorm/packs.dev/hello_st2# st2 rule list -p hello_st2
+---------------------------+-----------+-----------------------------------+---------+
| ref                       | pack      | description                       | enabled |
+---------------------------+-----------+-----------------------------------+---------+
| hello_st2.on_hello_event1 | hello_st2 | Sample rule firing on             | True    |
|                           |           | hello_st2.event1.                 |         |
+---------------------------+-----------+-----------------------------------+---------+

root@7afd86a716c4:/opt/stackstorm/packs.dev/hello_st2# st2 rule get hello_st2.on_hello_event1
+---------------+-----------------------------------------+
| Property      | Value                                   |
+---------------+-----------------------------------------+
| id            | 63b0c0e526171b55c61d7cfa                |
| uid           | rule:hello_st2:on_hello_event1          |
| ref           | hello_st2.on_hello_event1               |
| pack          | hello_st2                               |
| name          | on_hello_event1                         |
| description   | Sample rule firing on hello_st2.event1. |
| enabled       | True                                    |
| action        | {                                       |
|               |     "ref": "hello_st2.greet",           |
|               |     "parameters": {                     |
|               |         "greeting": "Yo"                |
|               |     }                                   |
|               | }                                       |
| context       |                                         |
| criteria      |                                         |
| metadata_file | rules/rule1.yaml                        |
| tags          |                                         |
| trigger       | {                                       |
|               |     "type": "hello_st2.event1",         |
|               |     "parameters": {},                   |
|               |     "ref": "hello_st2.event1"           |
|               | }                                       |
| type          | {                                       |
|               |     "ref": "standard",                  |
|               |     "parameters": {}                    |
|               | }                                       |
+---------------+-----------------------------------------+
```


## Sensor
```
root@7afd86a716c4:/opt/stackstorm/packs.dev/hello_st2# st2 sensor list -p hello_st2
+-----------------------+-----------+----------------------------------+---------+
| ref                   | pack      | description                      | enabled |
+-----------------------+-----------+----------------------------------+---------+
| hello_st2.HelloSensor | hello_st2 | Test sensor that emits triggers. | True    |
+-----------------------+-----------+----------------------------------+---------+

root@7afd86a716c4:/opt/stackstorm/packs.dev/hello_st2# st2 sensor get  hello_st2.HelloSensor
+---------------+-----------------------------------------------------------+
| Property      | Value                                                     |
+---------------+-----------------------------------------------------------+
| id            | 63b0c0e526171b55c61d7cf8                                  |
| uid           | sensor_type:hello_st2:HelloSensor                         |
| ref           | hello_st2.HelloSensor                                     |
| pack          | hello_st2                                                 |
| name          | HelloSensor                                               |
| enabled       | True                                                      |
| entry_point   | sensors.sensor1.HelloSensor                               |
| artifact_uri  | file:///opt/stackstorm/packs/hello_st2/sensors/sensor1.py |
| trigger_types | [                                                         |
|               |     "hello_st2.event1"                                    |
|               | ]                                                         |
| description   | Test sensor that emits triggers.                          |
| metadata_file | sensors/sensor1.yaml                                      |
+---------------+-----------------------------------------------------------+
```


## Trigger
```
root@7afd86a716c4:/opt/stackstorm/packs.dev/hello_st2# st2 trigger list -p hello_st2
+------------------+-----------+---------------------+
| ref              | pack      | description         |
+------------------+-----------+---------------------+
| hello_st2.event1 | hello_st2 | An example trigger. |
+------------------+-----------+---------------------+

root@7afd86a716c4:/opt/stackstorm/packs.dev/hello_st2# st2 trigger get hello_st2.event1
+-------------------+-------------------------------+
| Property          | Value                         |
+-------------------+-------------------------------+
| id                | 63b0c0e526171b55c61d7cf6      |
| ref               | hello_st2.event1              |
| pack              | hello_st2                     |
| name              | event1                        |
| description       | An example trigger.           |
| parameters_schema |                               |
| payload_schema    | {                             |
|                   |     "type": "object"          |
|                   | }                             |
| metadata_file     | sensors/sensor1.yaml          |
| tags              |                               |
| uid               | trigger_type:hello_st2:event1 |
+-------------------+-------------------------------+

root@7afd86a716c4:/opt/stackstorm/packs.dev/hello_st2# st2 trigger-instance list --trigger hello_st2.event1 -n 3
+--------------------------+------------------+----------------------------+-----------+
| id                       | trigger          | occurrence_time            | status    |
+--------------------------+------------------+----------------------------+-----------+
| 63b1627a6709baa4f995a661 | hello_st2.event1 | Sun, 01 Jan 2023 10:37:46  | processed |
|                          |                  | UTC                        |           |
| 63b162b66709baa4f995a66b | hello_st2.event1 | Sun, 01 Jan 2023 10:38:46  | processed |
|                          |                  | UTC                        |           |
| 63b162f26709baa4f995a675 | hello_st2.event1 | Sun, 01 Jan 2023 10:39:46  | processed |
|                          |                  | UTC                        |           |
+--------------------------+------------------+----------------------------+-----------+
+-----------------------------------------------------------------------------------------+
| Note: Only first 3 triggerinstances are displayed. Use -n/--last flag for more results. |
+-----------------------------------------------------------------------------------------+

root@7afd86a716c4:/opt/stackstorm/packs.dev/hello_st2# st2 trigger-instance get 63b162f26709baa4f995a675
+-----------------+------------------------------------+
| Property        | Value                              |
+-----------------+------------------------------------+
| id              | 63b162f26709baa4f995a675           |
| trigger         | hello_st2.event1                   |
| occurrence_time | 2023-01-01T10:39:46.090000Z        |
| payload         | {                                  |
|                 |     "greeting": "Yo, StackStorm!", |
|                 |     "count": 170                   |
|                 | }                                  |
| status          | processed                          |
+-----------------+------------------------------------+
```

## Policy
```
root@7afd86a716c4:/opt/stackstorm/packs.dev/hello_st2# st2 policy list -p hello_st2
+---------------------------+-----------------+--------------------+---------+
| ref                       | resource_ref    | policy_type        | enabled |
+---------------------------+-----------------+--------------------+---------+
| hello_st2.greet.concurren | hello_st2.greet | action.concurrency | True    |
| cy                        |                 |                    |         |
| hello_st2.http.retry      | core.http       | action.retry       | True    |
+---------------------------+-----------------+--------------------+---------+
```
