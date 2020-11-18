# REMS

The instace comes with demo database and fake login. These are NOT for production use. Information and documentation regarding rems: [https://github.com/CSCfi/rems](https://github.com/CSCfi/rems)

## Installing the Chart
The charts work out of the box with test configurations:

    helm install rems rems-helm

### Configuration
The charts are configured using files directory and values.yaml. Example files located under files/ directory. Configurable parameters in values.yaml:

                                    - General settings
hostname: fqdn                          - Hostname where REMS is reachable
protocol: http/https                    - Which protocol to use for connecting to REMS
port: number                            - Port number used for conneting to REMS
migrate: boolean                        - Run REMS migrate command or not
extraCommands: ""                       - Additional commands to be run
run: boolean                            - Start rems server or not

customConfig: boolean                   - If true using config file from files/config.edn (dont use different filename).
                                          If false using template file templates/rems-config.yaml and values.yaml
theme:
  create: boolean                       - Create theme configmaps using files found under files/theme/, files/img/
                                          and files/extra-translations/. Mount these configmaps to REMS pod and configure
                                          rems to use the theme.
extrapages:
  create: boolean                       - Create extra-pages configmap using files found under files/extra-pages,
                                          mount the configmap to REMS pod and configure REMS to use the configmap.
certs:
  create: false                         - Create configmap from certificates found under files/certs and mount them into
                                          rems pod. Currently one certificate is automatically to java certificate store.

ingress:                            - Ingress settings
  create: true                          - Create kubernetes ingress or not
  path: ""                              - Ingress path

postgres:                           - Local database settings
  create: boolean                       - Test postgres container to act as rems backend
  pvc: boolean                          - Persistent volume for the postgres instance
  storage: "1Gi"                        -Size of the persistent volume
db:                                 - General database settings
  name: string                          - Name of SQL database used as rems backend
  hostname: string                      - Hostname of the SQL database
  wait: boolean                         - Wait for database to be ready before starting REMS servier
  user: string                          - Username of database
  password: string                      - Password of the database user
  addData: boolean                      - Add test data to database. Requires an empty database
  addDataType: test-data/demo-data      - Which kind of test data to add ("test-data" and "demo-data" available)

image:                              - Docker image settings
  name: string                          - Image name/location
  tag: string                           - Image tag
  pullPolicy: Always/Never/IfNotPresent - Kubernetes ImagePullPolicy

