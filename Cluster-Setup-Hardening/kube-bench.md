## kube-bench

[Kube-bench](https://github.com/aquasecurity/kube-bench) is developed by The Aqua Security company to check whether Kubernetes is deployed as per security best practice


### how to download  (ARM64)

```
wget https://github.com/aquasecurity/kube-bench/releases/download/v0.13.0/kube-bench_0.13.0_linux_arm64.deb

```


```
sudo apt install ./kube-bench_0.13.0_linux_arm64.deb 
```

version check 

```
kube-bench version
```


### How to run kube-bench

```
sudo kube-bench run
```


results should be like below. Summary of the tests and remediation.

```
== Summary master ==

[INFO] 2 Etcd Node Configuration
[INFO] 2 Etcd Node Configuration
[FAIL] 2.1 Ensure that the --cert-file and --key-file arguments are set as appropriate (Automated)
[FAIL] 2.2 Ensure that the --client-cert-auth argument is set to true (Automated)
[FAIL] 2.3 Ensure that the --auto-tls argument is not set to true (Automated)
[FAIL] 2.4 Ensure that the --peer-cert-file and --peer-key-file arguments are set as appropriate (Automated)
[FAIL] 2.5 Ensure that the --peer-client-cert-auth argument is set to true (Automated)
[FAIL] 2.6 Ensure that the --peer-auto-tls argument is not set to true (Automated)
[WARN] 2.7 Ensure that a unique Certificate Authority is used for etcd (Manual)

== Remediations etcd ==
2.1 Follow the etcd service documentation and configure TLS encryption.
Then, edit the etcd pod specification file /etc/kubernetes/manifests/etcd.yaml
on the master node and set the below parameters.
--cert-file=</path/to/ca-file>
--key-file=</path/to/key-file>

2.2 Edit the etcd pod specification file /etc/kubernetes/manifests/etcd.yaml on the master
node and set the below parameter.
--client-cert-auth="true"

2.3 Edit the etcd pod specification file /etc/kubernetes/manifests/etcd.yaml on the master
node and either remove the --auto-tls parameter or set it to false.
  --auto-tls=false

== Summary master ==
1 checks PASS
46 checks FAIL
13 checks WARN
0 checks INFO


== Summary total ==
15 checks PASS
61 checks FAIL
57 checks WARN
0 checks INFO
```

### Try to a specific test using kube-bench

```
kube-bench --check="1.3.1"
```


```
kube-bench run --targets="master,etcd"
```