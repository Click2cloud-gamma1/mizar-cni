# mizar-cni
<div>
To deploy mizar cni, run this commands
  </div>
  <hr>
<pre>
sudo ls /etc/cni/net.d  
sudo rm /etc/cni/net.d/bridge.conf
kubectl apply -f https://raw.githubusercontent.com/Click2cloud-gamma1/mizar-cni/main/deploy.mizar.yaml
</pre>
