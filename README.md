# helm-charts
Configuration files for deploying various applications on Kubernetes clusters.

<table>
    <tbody>
        <tr>
            <th>LETS_ENCRYPT_EMAIL</th>
        </tr>
        <tr>
            <th>AIRFLOW_HOSTNAME</th>
        </tr>
        <tr>
            <th>AIRFLOW_FERNET_KEY</th>
        </tr>
        <tr>
            <th>AIRFLOW_SECRET_KEY</th>
        </tr>
        <tr>
            <th>AIRFLOW_USERNAME</th>
        </tr>
        <tr>
            <th>AIRFLOW_PASSWORD</th>
        </tr>
        <tr>
            <th>AIRFLOW_EMAIL</th>
        </tr>
        <tr>
            <th>AIRFLOW_FIRST_NAME</th>
        </tr>
        <tr>
            <th>AIRFLOW_LAST_NAME</th>
        </tr>
        <tr>
            <th>AIRFLOW_DAGS_REPO</th>
        </tr>
    </tbody>
</table>

```bash
curl -sfL https://get.k3s.io | sh -
sudo k3s kubectl get node
```

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/rancher/k3s/k3s.yaml $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
kubectl get nodes
```

```bash
#!/bin/bash
WEBSERVER_SECRET_KEY=$(openssl rand -base64 32)
FERNET_KEY=$(openssl rand -base64 32 | tr -d '\n')
echo "webserverSecretKey: $WEBSERVER_SECRET_KEY"
echo "fernetKey: $FERNET_KEY"
```

```bash
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/latest/download/cert-manager.yaml
```

```bash
envsubst < letsencrypt-cluster-issuer.yaml | kubectl apply -f -
```

```bash
helm repo add apache-airflow https://airflow.apache.org
helm repo update
```

```bash
envsubst < airflow-values.yaml | helm install airflow apache-airflow/airflow --namespace airflow --create-namespace --values -
```

```bash
helm uninstall airflow -n airflow
kubectl delete pvc -n airflow --all
kubectl delete namespace airflow
```