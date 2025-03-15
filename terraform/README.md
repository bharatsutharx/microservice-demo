
1. Initialize Terraform.

    ```bash
    terraform init
    ```

1. See what resources will be created.

    ```bash
    terraform plan
    ```

1. Create the resources and deploy the sample.

    ```bash
    terraform apply
    ```

    1. If there is a confirmation prompt, type `yes` and hit Enter/Return.

    Note: This step can take about 10 minutes. Do not interrupt the process.

Once the Terraform script has finished, you can locate the frontend's external IP address to access the sample application.

- Option 1:

    ```bash
    kubectl get service frontend-external | awk '{print $4}'
    ```

- Option 2: On Google Cloud Console, navigate to "Kubernetes Engine" and then "Services & Ingress" to locate the Endpoint associated with "frontend-external".

## Clean up

To avoid incurring charges to your Google Cloud account for the resources used in this sample application, either delete the project that contains the resources, or keep the project and delete the individual resources.

To remove the individual resources created for by Terraform without deleting the project:

1. Navigate to the `terraform/` directory.

1. Set `deletion_protection` to `false` for the `google_container_cluster` resource (GKE cluster).

   ```bash
   # Uncomment the line: "deletion_protection = false"
   sed -i "s/# deletion_protection/deletion_protection/g" main.tf

   # Re-apply the Terraform to update the state
   terraform apply
   ```

1. Run the following command:

   ```bash
   terraform destroy
   ```

   1. If there is a confirmation prompt, type `yes` and hit Enter/Return.
