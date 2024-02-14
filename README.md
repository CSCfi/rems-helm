# REMS Helm Charts

The instace comes with database dependency for PostgreSQL 13 (with demo credentials) and fake login. 
These are NOT for production use. 

Information and documentation regarding REMS is available at: [https://github.com/CSCfi/rems](https://github.com/CSCfi/rems)

## Installing the Charts

The charts work out of the box with test configurations:
```bash
git clone https://github.com/CSCfi/rems-helm
cd rems-helm
helm dependency build charts/rems
helm install rems charts/rems --set hostname="the.hostname.com",postgresql.auth.username="theuser",postgresql.auth.password="thepass"
```

Altenatively using helm repo:
```bash
helm repo add rems-helm https://cscfi.github.io/rems-helm/
helm search repo rems-helm
```
