```
https://argo-cd.readthedocs.io/en/stable/getting_started/
kubectl create namespace argocd
kubectl apply -n argocd --server-side --force-conflicts -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

### After installing You can check the service argocd-server make it as LoadBalancer
```
ubuntu@ip-172-31-33-216:~$ kubectl get svc -n argocd
NAME                                      TYPE           CLUSTER-IP       EXTERNAL-IP                                                               PORT(S)                      AGE
argocd-applicationset-controller          ClusterIP      172.20.57.179    <none>                                                                    7000/TCP,8080/TCP            4m29s
argocd-dex-server                         ClusterIP      172.20.149.250   <none>                                                                    5556/TCP,5557/TCP,5558/TCP   4m29s
argocd-metrics                            ClusterIP      172.20.62.8      <none>                                                                    8082/TCP                     4m29s
argocd-notifications-controller-metrics   ClusterIP      172.20.251.90    <none>                                                                    9001/TCP                     4m29s
argocd-redis                              ClusterIP      172.20.211.220   <none>                                                                    6379/TCP                     4m29s
argocd-repo-server                        ClusterIP      172.20.134.73    <none>                                                                    8081/TCP,8084/TCP            4m29s
argocd-server                             LoadBalancer   172.20.84.185    ac62015bd1d1e487296df3fe50b096cf-1816988299.us-west-2.elb.amazonaws.com   80:31319/TCP,443:30128/TCP   4m29s
argocd-server-metrics                     ClusterIP      172.20.69.17     <none>                                                                    8083/TCP                     4m29s
ubuntu@ip-172-31-33-216:~$

To Login to the console you can get the admin password from

1) ubuntu@ip-172-31-33-216:~$ kubectl get secret -n argocd
NAME                          TYPE     DATA   AGE
argocd-initial-admin-secret   Opaque   1      2m42s
argocd-notifications-secret   Opaque   0      3m59s
argocd-redis                  Opaque   1      2m51s
argocd-secret                 Opaque   5      3m59s

2) kubectl edit secrets argocd-initial-admin-secret -n argocd
3) echo MXhHbjJhQjE2cHF5aDZ4Ng== | base64 --decode
1xGn2aB16pqyh6x6
```
