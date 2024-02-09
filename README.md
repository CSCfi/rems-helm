# REMS

The instace comes with demo database and fake login. These are NOT for production use. Information and documentation regarding rems: [https://github.com/CSCfi/rems](https://github.com/CSCfi/rems)

## Installing the Charts
The charts work out of the box with test configurations:

    $ git clone https://github.com/CSCfi/rems-helm
    $ cd rems-helm
    $ helm dependency build
    $ helm install rems . --set hostname="the.hostname.com",postgresql.auth.username="theuser",postgresql.auth.password="thepass"

_Alternatively, you can edit the file `values.yaml`_:
  ```yaml
  hostname: "the.hostname.com"
  postgresql:
    auth:
      username: theuser
      password: thepassword
  ```

## Configuration files under `files/` directory

Example configuration files located under `files/` directory. Place custom configuration files in correct locations and set corresponding value `true` at `values.yaml` for the configuration to be applied in REMS. Configuration files and their corresponding value at `values.yaml`:


| Files(s) | value at `values.yaml | Explanation |
| -------------------------- | ------------------------ | -------------- |
| `files/config.edn` | customConfig | General REMS configuration
| `files/theme/*` | theme.create | General theme such as colors and logos |
| `files/img/*` | theme.create | Images used at theme configuration |
| `files/extra-translations/*` | theme.create | Custom texts |
| `files/extra-pages/*` | extrapages.create | Additional pages such as about pages |
| `files/certs/*` | certs.create | Certificates to be mounted into REMS pod |
| `files/keys/*` | keys.create | Keys to be mounted into REMS pod. |


## All Configurable parameters at `values.yaml`:

#### General settings

| Parameter | Possible values | Explanation |
| --------- | --------------- | ----------- |
| `name` | name | Name of your application |
| `orchestrator` | kubernetes/openshift | Container orchestartor used |
| `hostname` | hostname | Hostname of REMS. For instance, on CSC Rahti, it should be `rahtiapp.fi` (REQUIRED) |
| `readOnlyFilesystem` | boolean | Set true if kubernetes will be configured on read only filesystem. |
| `protocol` | http/https | Protocol to use for connecting to REMS |
| `port` | number | Port listened by REMS |
| `extraCommands` | command argument;command2 | Additional commands to be run spearated by semicolons (Works with rems `v2.14`->) |
| `run` | boolean  | Start rems server |
| `migrate` | boolean | Run REMS migrate commands before any other commands |
| `ingress.create` | boolean | Create kubernetes ingress (if `orchestrator` is `kubernetes`. Otherwise, create an OpenShift `route`) |
| `ingress.path:` | path | Ingress path |


#### PostgreSQL database settings

| Parameter | Possible values | Explanation |
| --------- | --------------- | ----------- |
| `postgresql.enabled` | boolean | Enable or not the use of PostgreSQL dependency (bitnami) |
| `postgresql.auth.username` | string | Set an username for the database (REQUIRED) |
| `postgresql.auth.password` | string | Set a password for the database (REQUIRED) |
| `postgresql.auth.database` | string | Name for a custom database in PostgreSQL |
| `postgresql.tls.enabled` | boolean | Enable or not tls support for the database |


#### REMS settings

| Parameter | Possible values | Explanation |
| --------- | --------------- | ----------- |
| `image.name` | string | Image name or location+name |
| `image.tag` | string | Image tag |
| `image.pullPolicy` | Always/Never/IfNotPresent | Kubernetes ImagePullPolicy |
| `database.addData` | boolean | Add test data to database. Requires a fresh and migrated database |
| `database.addDataType` | `test-data`/`demo-data` | Kind of test data to add |
| `customConfig` | boolean | If true using config file from `files/config.edn` (dont use different filename). If false using template file `templates/rems-config.yaml` and `values.yaml` |
| `theme.create` | boolean | Create theme configmaps using files found under `files/theme/`, `files/img/` and `files/extra-translations/`. Mount these configmaps to REMS pod and configure rems to use the theme. |
| `theme.filename` | string | Name of the theme's file to be used |
| `extrapages.create` | boolean | Create extra-pages configmap using files found under `files/extra-pages`, mount the configmap to REMS pod and configure REMS to use the configmap. |
| `extrapages.filename` | string | Name of the extra-pages's file to be used |
| `certs.create` | boolean | Create configmap from certificates found under `files/certs` and mount them into rems pod. Currently one certificate is automatically to java certificate store. |
| `keys.create` | boolean | Create secret from keys found under `files/keys` and mount them into rems pod. |
