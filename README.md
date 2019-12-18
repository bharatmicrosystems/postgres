# postgres
## Quick Start
```
git clone https://github.com/bharatmicrosystems/postgres.git
cd postgres
kubectl apply -f postgres-jiraconfluence.yaml
kubectl apply -f postgres-bitbucket.yaml
```
This would perform the following steps

Create a persistent volume called postgres-jiraconfluence-pv-volume and postgres-bitbucket-pv-volume with a path to /kubevolumes/postgres_data/jiraconfluence and /kubevolumes/postgres_data/bitbucket respectively. This would ensure that the postgres-jiraconfluence-data and postgres-bitbucket-data is persisted on disk even if the postgres containers goes down. The disk is replicated across all the nodes so the container can be scheduled to any of the nodes in the cluster

Create a persistent volume claim called postgres-jiraconfluence-pv-claim and postgres-bitbucket-pv-claim which binds with postgres-jiraconfluence-pv-volume and postgres-bitbucket-pv-volume respectively.

Create the postgres deployment which contains a reference to the official postgres container and the /postgres-data volume mounted to postgres-pv-claim.

Create a cluster IP service to expose the postgres UI to the kubernetes cluster

## Further setup
```
kubectl get pod|grep postgres-jiraconfluence
kubectl exec -it <POD> bash
su postgres
psql
create database jira2db;
create user jira2dbuser;
grant all privileges on database jira2db to jira2dbuser;
create database confluence2db;
create user confluence2dbuser;
grant all privileges on database confluence2db to confluence2dbuser;
exit
kubectl get pod|grep postgres-bitbucket
kubectl exec -it <POD> bash
su postgres
psql
create database bitbucketdb;
create user bitbucketdbuser;
grant all privileges on database bitbucketdb to bitbucketdbuser;
exit
```
