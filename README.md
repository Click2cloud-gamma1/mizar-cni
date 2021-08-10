# mizar-cni-health-criteria
<div>
To deploy mizar cni, run this commands
  </div>
  <hr>
<pre>
sudo ls /etc/cni/net.d  
sudo rm /etc/cni/net.d/bridge.conf
kubectl apply -f https://raw.githubusercontent.com/Click2cloud-gamma1/mizar-cni/main/deploy.mizar.yaml
</pre>
<hr>
<h3>
  test for successful mizar-cni deployment
 </h3>
 <hr>
 <div>
 check if node is ready if not restart containerd service
 <pre>
 sudo systemctl restart containerd.service
 </pre>
 </div>
 <div>
 check if vpcs, subnets,droplets,dividers,bouncers,endpoints are in provisoned state
 <pre>
 kubectl get vpcs
 kubectl get subnets
 kubectl get droplets
 kubectl get dividers
 kubectl get bouncers
 kubectl get endpoints
 </pre>
 </div>
 <div>
 Create test pod from netpod.yaml 
 <pre>
 kubectl apply -f https://raw.githubusercontent.com/Click2cloud-gamma1/mizar-cni/main/netpod.yaml
 </pre>
 </div>
 <div>
  Check if netpod1 and 3 can ping each other
  <pre>
  kubectl get pods -Ao wide
  </pre>
  <pre>
  NAMESPACE     NAME                             HASHKEY               READY   STATUS    RESTARTS   AGE     IP              NODE        NOMINATED NODE   READINESS GATES
default       mizar-daemon-hdl6k               8023306000523919195   1/1     Running   0          11m     192.168.1.242   centaurus   <none>           <none>
default       mizar-operator-d77985748-dlbf6   2807443624973927387   1/1     Running   0          11m     192.168.1.242   centaurus   <none>           <none>
default       netpod1                          5712308658918212290   1/1     Running   0          9m58s   20.0.0.5        centaurus   <none>           <none>
default       netpod2                          6008622540658758733   0/1     Pending   0          9m58s   <none>          <none>      <none>           <none>
default       netpod3                          3247207949606842015   1/1     Running   0          9m58s   20.0.0.25       centaurus   <none>           <none>
kube-system   kube-dns-554c5866fc-96zxz        7224918771882319920   3/3     Running   0          12m     10.88.0.42      centaurus   <none>           <none>
kube-system   virtlet-cbcdd                    6680824079774721614   3/3     Running   0          12m     192.168.1.242   
</pre>
  <pre>
  kubectl exec -it netpod1 -- sh
# ping 20.0.0.25
</pre>
 <pre>
PING 20.0.0.25 (20.0.0.25) 56(84) bytes of data.
64 bytes from 20.0.0.25: icmp_seq=1 ttl=64 time=0.144 ms
64 bytes from 20.0.0.25: icmp_seq=2 ttl=64 time=0.144 ms
</pre>
