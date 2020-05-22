# kind-with-metallb
Files for creating a kind cluster with metallb

[kind](https://github.com/kubernetes-sigs/kind) is great, but it comes without loadbalancer by default. [Duffie Cooley](https://github.com/mauilion) wrote this great tutorial how to integrate [metallb](https://github.com/metallb/metallb) into kind: https://mauilion.dev/posts/kind-metallb/

I automated the process of creating a multi-node kind cluster with metallb for myself. Putting these files up in case someone else finds them useful.
