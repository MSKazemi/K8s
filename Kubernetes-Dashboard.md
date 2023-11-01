apiVersion: v1
kind: Service
metadata:
  name: kubernetes-dashboard
  namespace: kube-system
spec:
  ports:
  - nodePort: 32691
    port: 443
    protocol: TCP
    targetPort: 8443
  selector:
    k8s-app: kubernetes-dashboard
  type: LoadBalancer