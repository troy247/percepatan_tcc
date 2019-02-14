1.
-Kubernetes adalah aplikasi cluster management open source. 

-kubectl untuk mengontrol cluster manager kubernet.

-POD Adalah satu grup container instance. Kita bisa menjalankan beberapa container (misalnya aplikasi web + redis cache + logging service) dalam satu pod.

 Antar container dalam satu pod bisa saling mengakses dengan menggunakan alamat localhost. Anggap saja pod seperti laptop yang kita 
 pakai coding. Untuk mengakses database dari aplikasi kita, biasanya kita pakai alamat localhost.
 
-Docker compose berfungsi untuk menjalankan container docker secara bersamaan.

-Docker Machine adalah tool yang untuk menginstal Docker Engine pada host virtual, dan mengelola 
 host dengan perintah docker machine.

2.
-Objek Kubernetes adalah entitas persisten dalam sistem Kubernetes.

-contoller adalah bertugas untuk memastikan status cluster sudah sesuai dengan status yang diamati.

-keterkaitan antara controller dan basic objek yaitu controller membangun di atas basic objeck.  

3.
-Secara default, kubernetes tidak memiliki dashboard akan tetapi kita dapat melakukan setup untuk kubernetes dashboard. Yang pertama 

kali dilakukan adalah 

 kita akan membuat sebuah file yaitu admin.yaml lalu isikan dengan source berikut.
 
 apiVersion: rbac.authorization.k8s.io/v1beta1
 
 kind: ClusterRoleBinding
 
 metadata:
  name: kubernetes-dashboard
  labels:
    k8s-app: kubernetes-dashboard
 roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
 subjects:
 - kind: ServiceAccount
   name: kubernetes-dashboard
   namespace: kube-system

Lalu jalankan perintah berikut untuk menambahkan user tersebut.

kubectl create -f admin.yaml

Setelah selesai, buat sebuah file dashboard.yaml

Lalu jalankan dashboard tersebut dengan perintah

kubectl apply -f dashboard.yaml

Hasilnya:

NAMESPACE     NAME                   TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)         AGE

default       kubernetes             ClusterIP   10.96.0.1       <none>        443/TCP         31m
 
kube-system   kube-dns               ClusterIP   10.96.0.10      <none>        53/UDP,53/TCP   31m
 
kube-system   kubernetes-dashboard   NodePort    10.101.10.168   <none>        443:31601/TCP   2m
 
Dari konfigurasi diatas, dapat dilihat bahwa kubernetes dashboard jalan pada port 31601, lalu silahkan akses kubernetes dashboard

di https://192.168.88.100:31601 seperti berikut.
