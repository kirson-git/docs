# Install the Run:AI Backend 

### Set Backend Configuration

Customize the Run:AI backend configuration file.

=== "Airgapped"
    Edit `runai-backend/runai-backend-helm-release.yaml`

=== "Connected"
    Generate a values file by running:
    ```
    runai-adm generate-values --openshift
    ```

## Edit Backend Configuration File

Change the following properties in the values file:


|  Replace |   With   | Description | 
|----------|----------|-------------| 
| `postgresql.persistence.nfs.server` | Set IP address for network file storage ||
| `postgresql.persistence.nfs.path` | Set path to dedicated Run:AI installation folder on NFS | path should be pre-created and have full access rights |
| `backend.initTenant.admin` | Change password for [admin@run.ai](mailto:admin.run.ai) | This user is the master Backend Administrator | 
| `backend.initTenant.users` | Change password for [test@run.ai](mailto:test@run.ai) | This user is the first cluster user | 
    |<img width=500/>|| 
 
<!-- | `tls.secretName` | name of Kubernetes secret under the runai-backend namespace | Secret contains certificate for `auth.runai.<company-name>` | -->


## Install Backend

Run the helm command below (replace `<version>` with the backend version):


=== "Airgapped"
    ```
    helm install runai-backend runai-backend/runai-backend-<version>.tgz -n \
        runai-backend -f runai-backend/runai-backend-helm-release.yaml 
    ```

=== "Connected"
    ```
    helm repo add runai-backend https://backend-charts.storage.googleapis.com
    helm repo update
    helm install runai-backend -n runai-backend \
        runai-backend/runai-backend -f <values-file> 
    ```


!!! Tip
    Use the  `--dry-run` flag to gain an understanding of what is being installed before the actual installation. 


## Connect to Administrator User Interface

Go to: `http://admin.<DOMAIN>`. Log in using the default credentials: User: `test@run.ai`, Password: `password`

## Next Steps

Continue with installing a [Run:AI Cluster](cluster.md).