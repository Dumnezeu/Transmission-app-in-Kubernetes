Follow the below steps to deploy Transmission App in Kubernetes using YAML files.

PREREQUISITES:

    l. Copy all of the above YAML files on a local directory
    2. Open communication on ports 30002, 30003, 30004 on the Router (or other ports, but they need to be modified in transm_deployment.yml).

DEPLOYMENT STEPS:

    l. Create namespace
        - kubectl create ns transmission

    2. Create the Storage Class
        - kubectl apply -f 1_transm_storageclass.yml -n transmission
     
    3. Create directories in the OS for the persistent volume
        - mkdir /downloads
        - mkdir /config
        - mkdir /watch
     
    4. Create the Persistent Volumes
        - kubectl create -f 2.1_transm_pv_downloads.yml -n transmission
        - kubectl create -f 2.2_transm_pv_config.yml -n transmission
        - kubectl create -f 2.3_transm_pv_watch.yml -n transmission
     
    5. Create the Persistent Volumes Claim
        - kubectl create -f 3.1_transm_pvc_downloads.yml -n transmission
        - kubectl create -f 3.2_transm_pvc_config.yml -n transmission
        - kubectl create -f 3.3_transm_pvc_watch.yml -n transmission
        
    6. Create the Secret to be used by the Transmission App
        - kubectl apply -f 4_transm_secret.yml -n transmission
	
    7. Deploy the transmission App
        - kubectl apply -f 5_transm_deployment.yml -n transmission

    8. Delete the Secret YAML file
        - rm -rf 4_transm_secret.yml
