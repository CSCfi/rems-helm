# REMS

The instace comes with demo database and fake login. These are NOT for production use. Information and documentation regarding rems: [https://github.com/CSCfi/rems](https://github.com/CSCfi/rems)

## Installing the Charts
The charts work out of the box with test configurations:

    git clone https://github.com/CSCfi/rems-helm
    helm install rems rems-helm

## Configuration
The charts are configured using files directory and values.yaml. Example files located under files/ directory. Configurable parameters in values.yaml:


#### General settings

| Parameter | Possible values | Explanation |
| --------- | --------------- | ----------- |
| hostname | hostname | Hostname of REMS |
| protocol | http/https | Protocol to use for connecting to REMS |
| port | number | Port listened by REMS |
| migrate | boolean | Run REMS migrate commands before any other commands |
| extraCommands | command argument;command2 | Additional commands to be run spearated by semicolons (Works with rems v2.14->) |
| run | boolean  | Start rems server |
| customConfig | boolean | If true using config file from files/config.edn (dont use different filename). If false using template file templates/rems-config.yaml and values.yaml |
| theme.create | boolean | Create theme configmaps using files found under files/theme/, files/img/ and files/extra-translations/. Mount these configmaps to REMS pod and configure rems to use the theme. |
| extrapages.create | boolean | Create extra-pages configmap using files found under files/extra-pages, mount the configmap to REMS pod and configure REMS to use the configmap. |
| certs.create | boolean | Create configmap from certificates found under files/certs and mount them into rems pod. Currently one certificate is automatically to java certificate store. |
| ingress.create | boolean | Create kubernetes ingress |
| ingress.path: | path | Ingress path |


#### Image settings

| Parameter | Possible values | Explanation |
| --------- | --------------- | ----------- |
| image.name | string | Image name or location+name |
| image.tag | string | Image tag |
| image.pullPolicy | Always/Never/IfNotPresent | Kubernetes ImagePullPolicy |


#### General database settings

| Parameter | Possible values | Explanation |
| --------- | --------------- | ----------- |
| db.name | string | Name of rems SQL backend database |
| db.hostname | hostname | Hostname of the SQL database |
| db.port | number | Port of the SQL database |
| db.wait | boolean | Wait for database to be ready before running REMS commands |
| db.user | string | Database username |
| db.password | string | Database user's password |
| db.addData | boolean | Add test data to database. Requires a fresh and migrated database |
| db.addDataType | test-data/demo-data | Kind of test data to add |


#### Local database settings

| Parameter | Possible values | Explanation |
| --------- | --------------- | ----------- |
| postgres.create | boolean | Create test postgres container to act as REMS backend |
| postgres.pvc | boolean |  Create persistent volume for the postgres instance |
| postgres.storage: | kubernetes size e.g "1Gi" | Size of the persistent volume |


