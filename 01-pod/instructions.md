# Exercise 1

In this exercise, you will practice the creation of a new Pod in a namespace. Once created, you will inspect it, shell into it and run some operations inside of the container.


1. Create the namespace `ckad-prep`.
2. In the namespace `ckad-prep`, create a new Pod named `mypod` with the image `nginx:2.3.5`. Expose the port 80.
3. Identify the issue with creating the container. Write down the root cause of issue in a file named `pod-error.txt`.
4. Change the image of the Pod to `nginx:1.15.12`.
5. List the Pod and ensure that the container is running.
6. Log into the container and run the `ls` command. Write down the output. Log out of the container.
7. Retrieve the IP address of the Pod `mypod`.
8. Run a temporary Pod in the namespace `ckad-prep` using the image `busybox`, shell into it and run a `wget` command against the `nginx` Pod using port 80.
9. Render the logs of Pod `mypod`.
10. Delete the Pod and the namespace.

2.kubectl run mypod --image=nginx:2.3.5 --port=80 --namespace=ckad-prep ensuite k describe pod -n
3.D'après les événements, l'erreur se produit lors de la récupération de l'image nginx:2.3.5 à partir du registre docker.io/library. 
L'erreur est docker.io/library/nginx:2.3.5: not found.
La cause de l'erreur est que l'image nginx:2.3.5 n'existe pas sur le registre Docker docker.io/library. 
Il est possible que l'image ait été supprimée ou renommée.
4.kubectl set image pod/mypod nginx:1.15.12 -n ckad-prep
5.k get pod -o wide
6.k exec mypod -it -n ckad-prep -- /bin/sh ensuite faire ls
7. 10.233.91.209
8. 
9. k log mypod -n 