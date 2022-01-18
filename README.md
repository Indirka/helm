Helm
   
1) Create a helm chart with the hook-job that runs only once and deployment with 3 replicas
  helm install demo test
  helm upgrade demo test-chart
  helm uninstall demo test-chart

2) Create  service 
  kubectl create test-svc.yaml
  kubectl get ep test-svc

3) Generate Self-Signed Certificates for the Service and Store Them in a Secret:
  openssl req -nodes -new -x509 -keyout test.key -out test.crt -subj "/CN=test.svc"
  kubectl create secret tls test-tls --cert=test.crt --key=test.key

4) Create an Ingress on Top of the Service That Configures TLS Termination:
  kubectl create -f test-tls-ingress.yml
  kubectl describe ingress test-tls-ingress
