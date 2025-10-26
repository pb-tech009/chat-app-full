       <!-- # enter in the pod you want  -->
        # kubectl exec -it mongodb-0 -n chat-app -- bash
        # mongosh -u mongoadmin -p secret --authenticationDatabase admin

# show dbs
# use dbname
# users
# messages
# db.users.find().pretty()
# {
#   "_id": ObjectId("6716b3c7f48d..."),
#   "username": "parth",
#   "email": "parth@example.com",
#   "password": "..."
# }

# db.messages.find().pretty()
# {
#   "_id": ObjectId("6716b4f7f48d..."),
#   "sender": "parth",
#   "receiver": "sam",
#   "message": "Hey there!",
#   "timestamp": "2025-10-21T09:00:00Z"
# }

# exit
# exit

<!-- this is for the vpa [vertical pod autoscale ] -->
  # kubectl apply -f https://raw.githubusercontent.com/kubernetes/autoscaler/master/vertical-pod-autoscaler/deploy/vpa-v1-crd-gen.yaml

  #  kubectl apply -f https://raw.githubusercontent.com/kubernetes/autoscaler/master/vertical-pod-autoscaler/deploy/vpa-rbac.yaml


<!-- this is for the HPA [horizontal pod autoscale] -->
#  kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
# kubectl -n kube-system edit deployment metrics-server
# add this into container and make correct the indentation but in this i also made and metrix-server-kind.yml so you ca direct apply this 
# - --kubelet-insecure-tls
# - --kubelet-preferred-address-types=InternalIP,Hostname,ExternalIP

in this ypu dont need to make any or i just made in this an a metrix-server-kind.yaml so you just need to run this  
# kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
and then just apply this 
#  metrix-server-kind.yaml 
and then direct check this 
 # kubectl top nodes


 <!-- NOW THE GENERATE THE LOAD ON THE ANYTHING OU WANT SO TYPE THIS CMD LIKE -->

 # kubectl run -i --tty load-generator --image-busybox -n apache /bin/sh
 while true; do wget -q -o https://apache-service.apache.svc.cluster.local; done


 
 <!-- ROLEBACK ACCESS CONTROL -->

 PS G:\kubernetes\chat-app\full-stack_chatApp\k8s> kubectl auth whoami
ATTRIBUTE                                           VALUE
Username                                            kubernetes-admin
Groups                                              [kubeadm:cluster-admins system:authenticated]
Extra: authentication.kubernetes.io/credential-id   [X509SHA256=a690c4665dbeb6628aa4c56f113a855cc1b75c1d048787c9fb2b3acf6ba75e31]
PS G:\kubernetes\chat-app\full-stack_chatApp\k8s> kubectl auth can-i get pods -n chat-app
yes


then you can apply all your yml and then you can see this like go in the service account whe you made and on this svc acount you can see the name 
apiVersion: v1
kind: ServiceAccount
metadata:
# name:  manager-svc
  namespace: chat-app
  manager-svc  see this and then you can all bing your then you can see this all vy this cmd 
  # kubectl auth can-i get pods --as=manager-svc -n chat-app
 

 <!-- dashbord for the kind cluster  -->
# kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.7.0/aio/deploy/recommended.yaml
then appy our role-dashbord-admin.yml


<!-- this apply then make an tolen so you can acces this and get this  -->
# kubectl -n kubernetes-dashboard create token admin-user
then you can apply this so they gave you an a huge token so you can copy thet token and save that to the safe place so you can accces your dashbord 
--then apply this cmd = kubectl proxy --port=8001 --address=0.0.0.0 --accept-host='.*' 
# then you can see this like a  = Starting to serve on [::]:8001  
then go on the browser and run this  =  http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/  




