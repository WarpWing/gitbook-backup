---
description: Working with Memphis CLI
---

# Usage

## Usage

### Connect

{% hint style="success" %}
Once connected, all features offered by Memphis are available.
{% endhint %}

#### Connection to Memphis control plane:

```powershell
$ mem connect -s <cmemphis broker> -u root -p memphis
```

#### Required parameters:

```powershell
-u, --user                 User
-p, --password <password>  Password
-s, --server <server>      Memphis broker
-h, --help                 display help for command
```

#### Example:

```powershell
$ mem connect -u root -p memphis -s http://localhost:9000                       
Connected successfully to Memphis control plane.
```

### Stations

{% hint style="info" %}
A station is Memphis' version of a queue/topic/channel/subject.
{% endhint %}

```powershell
$ mem station <command> [options]
```

#### Station commands:

```powershell
   ls                List of stations
   create            Create new station  
   info              Specific station's info
   del               Delete a station
```

#### Station options:

```powershell
  -f, --factory <factory>                  Factory name
  -rt, --retentiontype <retention-type>    Retention type
  -rv, --retentionvalue <retention-value>  Retention value
  -s, --storage <storage-type>             Storage type
  -r, --replicas <replicas>                Replicas
  -ipw, --idempotency <idempotency-window-in-ms>  Idempotency window in ms
  -h, --help                               display help for command
```

#### Examples:

```powershell
$ mem station ls                 
┌─────────┬────────┬────────────────┬────────────────────┬──────────────┬──────────┬───────────────────────┬────────────┬───────────────┬──────────────┐
│ (index) │  name  │ retention type │ retentention value │ storage type │ replicas │ idempotency window ms │ created by │ creation date │ last_update  │
├─────────┼────────┼────────────────┼────────────────────┼──────────────┼──────────┼───────────────────────┼────────────┼───────────────┼──────────────┤
│    0    │ 'test' │   'messages'   │       604800       │    'disk'    │    1     │        120000         │   'root'   │ '2022-12-04'  │ '2022-12-04' │
└─────────┴────────┴────────────────┴────────────────────┴──────────────┴──────────┴───────────────────────┴────────────┴───────────────┴──────────────┘
```



```powershell
$ mem station create mystation
Station mystation was created with the following details:
┌─────────┬─────────────┬───────────────────┬────────────────────┬──────────────┬──────────┬───────────────────────┬────────────┬───────────────┐
│ (index) │    name     │  retention type   │ retentention value │ storage type │ replicas │ idempotency window ms │ created by │ creation date │
├─────────┼─────────────┼───────────────────┼────────────────────┼──────────────┼──────────┼───────────────────────┼────────────┼───────────────┤
│    0    │ 'mystation' │ 'message_age_sec' │       604800       │    'disk'    │    1     │        120000         │   'root'   │ '2022-12-04'  │
└─────────┴─────────────┴───────────────────┴────────────────────┴──────────────┴──────────┴───────────────────────┴────────────┴───────────────┘

$ mem station ls
┌─────────┬─────────────┬───────────────────┬────────────────────┬──────────────┬──────────┬───────────────────────┬────────────┬───────────────┬──────────────┐
│ (index) │    name     │  retention type   │ retentention value │ storage type │ replicas │ idempotency window ms │ created by │ creation date │ last_update  │
├─────────┼─────────────┼───────────────────┼────────────────────┼──────────────┼──────────┼───────────────────────┼────────────┼───────────────┼──────────────┤
│    0    │   'test'    │    'messages'     │       604800       │    'disk'    │    1     │        120000         │   'root'   │ '2022-12-04'  │ '2022-12-04' │
│    1    │ 'mystation' │ 'message_age_sec' │       604800       │    'disk'    │    1     │        120000         │   'root'   │ '2022-12-04'  │ '2022-12-04' │
└─────────┴─────────────┴───────────────────┴────────────────────┴──────────────┴──────────┴───────────────────────┴────────────┴───────────────┴──────────────┘
```



```powershell
$ mem station info mystation
Station info:
{
  id: '638cad761ba211dc5dc1ae96',
  name: 'mystation',
  retention_type: 'message_age_sec',
  retention_value: 604800,
  storage_type: 'disk',
  replicas: 1,
  dedup_enabled: false,
  dedup_window_in_ms: 0,
  created_by_user: 'root',
  creation_date: '2022-12-04T14:23:50.037Z',
  last_update: '2022-12-04T14:23:50.037Z',
  functions: [],
  is_deleted: false,
  tags: [],
  idempotency_window_in_ms: 120000
}
```

```powershell
$ mem station del mystation
Statoin mystation was removed.

$ mem station ls
┌─────────┬────────┬────────────────┬────────────────────┬──────────────┬──────────┬───────────────────────┬────────────┬───────────────┬──────────────┐
│ (index) │  name  │ retention type │ retentention value │ storage type │ replicas │ idempotency window ms │ created by │ creation date │ last_update  │
├─────────┼────────┼────────────────┼────────────────────┼──────────────┼──────────┼───────────────────────┼────────────┼───────────────┼──────────────┤
│    0    │ 'test' │   'messages'   │       604800       │    'disk'    │    1     │        120000         │   'root'   │ '2022-12-04'  │ '2022-12-04' │
└─────────┴────────┴────────────────┴────────────────────┴──────────────┴──────────┴───────────────────────┴────────────┴───────────────┴──────────────┘
```

### Users

{% hint style="info" %}
You can manage users and permissions.
{% endhint %}

```powershell
$ mem user <command> [options]
```

#### User commands:

```powershell
   ls                List of users
   add               Add new user  
   del               Delete user
```

#### User options:

```powershell
  -u, --username <username>          Username
  -p, --password <user-password>  User password
  -t, --type <user-type>          User type (default: "management") - application/management
  -a, --avatar <avatar-id>        Avatar id (default: 1) -  1-4
  -h, --help                      display help for command
```

#### Examples:

```powershell
$ mem user ls
┌─────────┬───────────┬────────────────────────────┬───────────┐
│ (index) │ user_name │       creation_date        │ user_type │
├─────────┼───────────┼────────────────────────────┼───────────┤
│    0    │  'root'   │ '2022-04-18T12:38:47.034Z' │  'root'   │
└─────────┴───────────┴────────────────────────────┴───────────┘
```

```powershell
$ mem user add --name shay --password 123456
{ type: 'management', avatar: 1, name: 'shay', password: '123456' }
User shay was created.
```

```powershell
$ mem user add --ame sveta --type application --avatar 3 
{ type: 'application', avatar: '3', name: 'sveta' }
User sveta was created.
Broker connection credentials: imeD5g08Bz8mbJavU4zi
These credentials CANT be restored, save them in a safe place

$ mem user ls
┌─────────┬───────────┬────────────────────────────┬───────────────┐
│ (index) │ user_name │       creation_date        │   user_type   │
├─────────┼───────────┼────────────────────────────┼───────────────┤
│    0    │  'root'   │ '2022-04-18T12:38:47.034Z' │    'root'     │
│    1    │  'shay'   │ '2022-04-20T13:54:32.571Z' │ 'management'  │
│    2    │  'sveta'  │ '2022-04-20T13:56:46.589Z' │ 'application' │
└─────────┴───────────┴────────────────────────────┴───────────────┘
```

```powershell
$ mem user del shay
User shay was removed.

$ mem user ls
┌─────────┬───────────┬────────────────────────────┬───────────────┐
│ (index) │ user_name │       creation_date        │   user_type   │
├─────────┼───────────┼────────────────────────────┼───────────────┤
│    0    │  'root'   │ '2022-04-18T12:38:47.034Z' │    'root'     │
│    1    │  'sveta'  │ '2022-04-20T14:01:38.494Z' │ 'application' │
└─────────┴───────────┴────────────────────────────┴───────────────┘
```

### Producers

{% hint style="info" %}
A producer is an entity that can send messages into stations.
{% endhint %}

#### Producer commands:

```powershell
   ls                List of Producers
```

#### Producer options:

```powershell
  -s, --station <station-name>  Producers by station
  -h, --help                    display help for command
```

#### Examples:

```powershell
$ mem producer ls
┌─────────┬──────┬──────┬─────────────────┬──────────────┬──────────────┬───────────────┐
│ (index) │ name │ type │ created_by_user │ station_name │ factory_name │ creation_date │
├─────────┼──────┼──────┼─────────────────┼──────────────┼──────────────┼───────────────┤
│    0    │ ' '  │ ' '  │       ' '       │     ' '      │     ' '      │      ' '      │
└─────────┴──────┴──────┴─────────────────┴──────────────┴──────────────┴───────────────┘
```

### Consumers

{% hint style="info" %}
A consumer is an entity that can consume messages from stations.
{% endhint %}

#### Consumer commands:

```powershell
   ls                List of Consumers
```

#### Consumer options:

```powershell
  -s, --station <station-name>  Consumers by station
  -h, --help                    display help for command
```

#### Examples:

```powershell
$ mem consumer ls
┌─────────┬──────┬──────┬────────────────┬─────────────────┬──────────────┬──────────────┬───────────────┐
│ (index) │ name │ type │ consumer_group │ created_by_user │ station_name │ factory_name │ creation_date │
├─────────┼──────┼──────┼────────────────┼─────────────────┼──────────────┼──────────────┼───────────────┤
│    0    │ ' '  │ ' '  │      ' '       │       ' '       │     ' '      │     ' '      │      ' '      │
└─────────┴──────┴──────┴────────────────┴─────────────────┴──────────────┴──────────────┴───────────────┘
```

### Get a code snippet

{% hint style="info" %}
Creates an example project for working with Memphis.
{% endhint %}

#### Examples:

```powershell
$ mem init

'mem init' creates an example project for connecting an app with Memphis.

The default language is nodejs.
If you want to use different language use 'mem init -l/--language <language>'.
Currently supported languages: nodejs.

For more help use 'mem init -h'.

The project will be created in directory /Users/myUser/myCurrentDir
 continue? Y/n
index.js was created.
```



### Cluster info

{% hint style="info" %}
Information about your Memphis cluster.
{% endhint %}

#### Examples:

```powershell
$ mem cluster info

Cluster Info:

Memphis version: 0.4.2

```
