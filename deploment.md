
# Replicaset and Deployment.yml

Replication Controller:

```yaml
#rc.yml
apiversion: v1
kind: ReplicationController 
metadata:
	name: nginx-rc
	labels:
		env: demo
spec:
	template:
	  metadata:
		  labels:
			  env: demo
			  name: nginx
		spec:
			containers:
				- image: nginx
					name: nginx
					ports:
						- containerPort: 80
	replicas: 3
#kubectl apply -f rc.yml
#kubectl get rc
#kubectl describe podname
```

ReplicaSet

```yaml
apiversion: apps/v1
kind: ReplicaSet
metadata:
	name: nginx-rs
	labels:
		env: demo
spec:
	template:
		metadata:
			labels:
				env: demo
				name: nginx-rs
	spec:
		containers:
			- image: nginx
				name: nginx
				ports:
					- containerport: 80
	replicas: 3
	selector: 
		matchLabels:
			env: demo
			
#kubectl explain rs
#kubectl apply -f rs.yml
#kubectl get rs
#kubectl scale --replicas=10 podname

					
						
```

We can manage the existing pods as well using selector 

## Deployement —> Replicaset

**deployment.yml**

```yaml
apiversion: apps/v1
kind: deployment
metadata:
	name: nginx-deployment
	labels:
		env: demo
spec:
	template:
	metadata:
		labels:
			name: nginx-deployment
			env: demo
	spec:
		containers:
			- image: nginx
				name: nginx-deploy
				ports:
					- containerport: 80
	replicas: 3
	selector:
		matchLabels:
			env: demo
			
	#kubectl apply -f deployment.yml
	#kubectl get all
	#kubectl set image deploy/nginx-deploy \
	 # nginx=naginx:1.9.1
	#kubectl describe  imagename
	#kubectl rollout history imagename
	 

```
