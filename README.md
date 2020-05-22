# kind-with-metallb

Files for creating a kind cluster with metallb

[kind](https://github.com/kubernetes-sigs/kind) is great, but it comes without loadbalancer by default. [Duffie Cooley](https://github.com/mauilion) wrote this great tutorial how to integrate [metallb](https://github.com/metallb/metallb) into kind: [https://mauilion.dev/posts/kind-metallb/](https://mauilion.dev/posts/kind-metallb/)

I automated the process of creating a multi-node kind cluster with metallb for myself. Putting these files up in case someone else finds them useful.

## To use

Usage: `./kind-with-metallb <kind config> <metallb config>`

With the example files:
`./kind-with-metallb multinodecluster.yaml kind-metallb-config.yaml`

## To test

To test the setup apply the content of the `demo` directory:

```bash
$ kubectl apply -f demo/
deployment.apps/echo created
service/echo created
```

Use `kubectl get all` to see what was created:

```bash
 k get all
NAME                       READY   STATUS    RESTARTS   AGE
pod/echo-56f77f694-5k56c   1/1     Running   0          9m8s
pod/echo-56f77f694-kskpd   1/1     Running   0          9m8s
pod/echo-56f77f694-kxnzp   1/1     Running   0          9m8s

NAME                 TYPE           CLUSTER-IP      EXTERNAL-IP    PORT(S)          AGE
service/echo         LoadBalancer   10.96.222.109   172.17.255.1   8080:32353/TCP   9m8s
service/kubernetes   ClusterIP      10.96.0.1       <none>         443/TCP          54m

NAME                   READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/echo   3/3     3            3           9m8s

NAME                             DESIRED   CURRENT   READY   AGE
replicaset.apps/echo-56f77f694   3         3         3       9m8s
```

Now connect your browser to [http://172.17.255.1:8080](http://172.17.255.1:8080) and reload the page repeatedly. You should see the output from all three pods eventually.
(Make sure to bypass the cache - e.g. press `Ctrl-F5` in firefox.)
