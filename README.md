Follow the below steps to deploy Transmission App in Kubernetes using YAML files.

First copy all of the YAML files on a local directory.

DEPLOYMENT STEPS:

    l. Create namespace
        - kubectl create ns transmission

    2. Create the Storage Class
        - kubectl apply -f transm_storageclass.yml -n transmission
     
    3. Create directories in the OS for the persistent volume
        - mkdir /config
        - mkdir /downloads
        - mkdir /watch
     
    4. Create the Persistent Volumes
        - kubectl create -f transm_pv_config.yml -n transmission
        - kubectl create -f transm_pv_downloads.yml -n transmission
        - kubectl create -f transm_pv_watch.yml -n transmission
     
    5. Create the Persistent Volumes Claim
        - kubectl create -f transm_pvc_config.yml -n transmission
        - kubectl create -f transm_pvc_downloads.yml -n transmission
        - kubectl create -f transm_pvc_watch.yml -n transmission
        
    6. Create the Secret to be used by the Transmission App
        - kubectl apply -f transm_secret.yml -n transmission
	
    7. Deploy the transmission App
        - kubectl apply -f transm_deployment.yml -n transmission

    8. Delete the Secret YAML file
        - rm -rf transm_secret.yml
