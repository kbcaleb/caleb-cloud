---
title: "Deploying to Kubernetes"
---
Now that you have Kubernetes running lets deploy a simple demo WordPress app to your cluster.


```yaml
apiVersion: v1
kind: Service
metadata:
  name: wordpress-mysql
  labels:
    app: wordpress
spec:
  ports:
    - port: 3306
  selector:
    app: wordpress
    tier: mysql
  clusterIP: None
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mysql-pv-claim
  labels:
    app: wordpress
  spec:
    accessModes:
      - ReadWriteOnce
    resources:
      requests:
        storage: 20Gi
---
apiVersion: apps/v1
kind: Deploymnet
metadata:
  name: wordpress
  tier: mysql  
strategy:
  type: Recreate
template:
  metadata:
    labels:
      app: wordpress
      tier: mysql
  spec:
    containers:
    - image: mysql:5.7
      name: mysql
      env:
      - name: MYSQL_ROOT_PASSWORD
        valueFrom:
          secretKeyRef:
            name: mysql-pass
            key: password
      ports:
      - containerPort: 3306
        name: mysql
      volumeMounts:
      - name: mysql-persistent-storage
        mountPath: /var/lib/mysql
    volumes:
    - name: mysql-persistent-storage
      persistentVolumeClaim:
        claimName: mysql-pv-claim
```
