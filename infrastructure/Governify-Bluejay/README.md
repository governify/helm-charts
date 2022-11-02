
# CONFIGURATION PARAMETERS

> **Note**
>
> The default namespace for this infrastructure is `governify-bluejay`

## GLOBAL CONFIGURATION

| **Name**           	| **Required** 	| **Type** 	| **Default** 	| **Description**                                   	|
|--------------------	|--------------	|----------	|:-----------:	|---------------------------------------------------	|
| services_prefix    	| only_prod    	| String   	| -           	| The DNS prefix that services will use             	|
| dns_suffix         	| only_prod    	| String   	| -           	| The DNS suffix that services will use             	|
| node_env           	| yes          	| String   	|  production 	| The environment in which the app will be deployed 	|
| infrastructure     	| yes          	| String   	|    falcon   	| The infrastructure name                           	|
| gov_infrastructure 	| yes          	| String   	| -           	| URL to **infrastructure** file in assets-manager  	|
| login_user         	| yes          	| String   	| -           	| Render and Assets Manager login user              	|
| login_password     	| yes          	| String   	| -           	| Render and Assets Manager login password          	|
| namespaceOverride    	| no          	| String   	| -           	| Override default namespace                          	|

## SERVICES CONFIGURATION

### Assets Manager

| **Name**                 	| **Required** 	| **Type** 	|             **Default**            	| **Description**                                  	|
|--------------------------	|--------------	|----------	|:----------------------------------:	|--------------------------------------------------	|
| private_key              	| yes          	| String   	| defaultkey                         	| Assets Manager key for private directory         	|
| assets_repository        	| yes          	| String   	| github.com/governify/assets-falcon 	| Repository that will be cloned by Assets Manager 	|
| assets_repository_branch 	| yes          	| String   	| main                               	| Repository branch that will be cloned            	|
| gov_infrastructure       	| yes          	| String   	| -                                  	| Assets local path to infrastructure file         	|
| volume_storage       	| yes          	| String   	| 5Gi                                  	| Assets volume capacity          	|

### Scope Manager

| **Name**                 	| **Required** 	| **Type** 	|             **Default**            	| **Description**                                  	|
|--------------------------	|--------------	|----------	|:----------------------------------:	|--------------------------------------------------	|
| private_key              	| yes          	| String   	| defaultkey                         	| Scope Manager access key         	|


### Influx DB

| **Name**                 	| **Required** 	| **Type** 	|             **Default**            	| **Description**                                  	|
|--------------------------	|--------------	|----------	|:----------------------------------:	|--------------------------------------------------	|
| volume_storage       	| yes          	| String   	| 5Gi                                  	| InfluxDB volume capacity          	|

### Mongo DB

| **Name**                 	| **Required** 	| **Type** 	|             **Default**            	| **Description**                                  	|
|--------------------------	|--------------	|----------	|:----------------------------------:	|--------------------------------------------------	|
| volume_storage       	| yes          	| String   	| 5Gi                                  	| InfluxDB volume capacity          	|

### Collector events

| **Name**                 	| **Required** 	| **Type** 	|             **Default**            	| **Description**                                  	|
|--------------------------	|--------------	|----------	|:----------------------------------:	|--------------------------------------------------	|
| key_github              	| yes          	| String   	| -                         	| Github Token|
| key_pivotal              	| yes          	| String   	| -                         	| Pivotal Token|
| key_travis_public         | yes           | String   	| -                        | Travis public key|
| key_travis_private        | yes           | String   	| -                        | Travis private key|
| key_heroku                | yes           | String   	| -                        | Heroku token|
| key_codeclimate           | yes           | String   	| -                        | Codeclimate token|
