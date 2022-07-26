# Traefik_Test
Test of traefik reverse proxy

Traefik is an Edge Router, it means that it's the door to your platform, and that it intercepts and routes every incoming request: it knows all the logic and every rule that determine which services handle which requests (based on the path, the host, headers, and so on ...).

# 1) launch traefik instance up and running
launch traefik: docker run -d -p 8080:8080 -p 80:80 -v $PWD/traefik.yml:/etc/traefik/traefik.yml -v /var/run/docker.sock:/var/run/docker.sock traefik:v2.5 

# 2)start backend servers
start backend server 1: docker run -d --name first traefik/whoami

start backend server 2: docker run -d --name second traefik/whoami

# What happen ?

first we create a traefik instance.
Then we start some backend servers and we connect them to traefik who automaticaly create path to them like:

localhost (traefik)
 
 -- first.localhost (first backend server)
 
 -- second.localhost (second backend server)
 
 
 # Troubleshoot
 
 When testing this reverse proxy
 I was facing an issue this docker desktop it was stuk on Starting State.
 
 I tested many option found on stackoverflow nothing works. 
 
 Finally i find this usefull instruction that solve momentanelly the problem.
 https://dev.to/ivanauliaa/when-my-docker-desktop-stuck-on-starting-state-nda
 
 the origin of blocking on starting state was Hyper-V Manager and its solved by
 
 1) stoping Hyper-V: type Hyper-V Manager in windows search
 2) retarting PC
 3) manually stop and rm any docker contenair
 
