## Enable Dashboard
`microk8s enable dashboard`

## Change the Type of Service
`kubectl edit svc -n kube-system kubernetes-dashboard`

Change `type: ClusterIP` to `type: NodePort`

OR:

## Add External Service
```yaml
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
```
