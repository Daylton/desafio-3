# 1 - Start/Iniciar a máquina virtual bastion


# 2 - Definir as variáveis

````
export SSH_IAP_NETWORK_TAG=
````

````
export SSH_INTERNAL_NETWORK_TAG=
````

````
export HTTP_NETWORK_TAG=
````

````
export ZONE=
````


# 3 - Executar os comandos,  1 de cada vez. Lembrar de esperar terminar para executar o próximo


````
gcloud compute firewall-rules delete open-access
````
 ````
gcloud compute firewall-rules create ssh-ingress --allow=tcp:22 --source-ranges 35.235.240.0/20 --target-tags $SSH_IAP_NETWORK_TAG --network acme-vpc
````
 ````
gcloud compute instances add-tags bastion --tags=$SSH_IAP_NETWORK_TAG --zone=$ZONE
```` 
````
gcloud compute firewall-rules create http-ingress --allow=tcp:80 --source-ranges 0.0.0.0/0 --target-tags $HTTP_NETWORK_TAG --network acme-vpc
````````
 ````
gcloud compute instances add-tags juice-shop --tags=$HTTP_NETWORK_TAG --zone=$ZONE
````
 
````
gcloud compute firewall-rules create internal-ssh-ingress --allow=tcp:22 --source-ranges 192.168.10.0/24 --target-tags $SSH_INTERNAL_NETWORK_TAG --network acme-vpc
````

```` 
gcloud compute instances add-tags juice-shop --tags=$SSH_INTERNAL_NETWORK_TAG --zone=$ZONE
 ````
  
# 4 - Acessar a bastion via SSH e executar o comando a seguir dentro dela

````
gcloud compute ssh juice-shop --internal-ip
````

# Ao pedir passphrase, só teclar enter
# Quando pedir para confirmar a passphrase, tecla enter novamente


# Quando aparecer a pergunta : Did you mean zone [...] for instance: [juice-shop] (Y/n), responda com y e tecla enter

