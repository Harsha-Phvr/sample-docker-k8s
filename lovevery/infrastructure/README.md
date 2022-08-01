
## Create infrastructure in the newly created environment folder structure also helps with managing statefiles
Run the following commands to create the resources with Terraform:
```bash
cd environments/<your_desired_env>
terraform init
terraform plan --out=output.tfplan
terraform apply output.tfplan
```

<!-- ## Project structure

```
├── environments                            # Contains environment specific files
│   ├── 0_development                       # Files specific to development environment
│   │   ├── development.auto.tfvars.backup  # variable template. Copy to development.auto.tfvars
│   │   ├── provider.tf.ts                  # This is to handle output variables
│   │   └── ...                             # Environment specific files
│   └── ...                                 # Other environments such as 1_test, 2_stage, etc.
├── manifests                               # Contains common files
│   ├── variables.ts                        # Common variables with defaults
│   ├── provider.ts                         # Provider declaration
│   ├── vpc.ts                              # VPC declaration
│   └── ...                                 # Other declarations such as ec2, cognito, s3, etc.
└── README.md
``` -->

## Initial developer setup for <env> `dev`, `test`,  `prod`

1. Go to the specific environment folder
    ```bash
    cd environments/<env>
    ```
2. [one-time only] Copy `<env>.auto.tfvars.example` to `<env>.auto.tfvars`, and fill in the variables
3. [one-time only] Set aws profile to initialize the backend
    ```bash
    export AWS_PROFILE=<env>-user
    ```
4. [one-time only] Initialize the backend for terraform state management
    ```bash
    terraform init -backend-config="backend/<env>.tfvars"
    ```
5. Run terraform plan with environment specific configs which is defined at `env_vars/<env>.tfvars`
    ```bash
    terraform fmt # clean up terraform styles
    terraform plan -var-file="env_vars/<env>.tfvars"
    ```
    > use `-lock=false` to disable locking temporarily
    > TODO: fix issue with bastion count error
6. Deploy the changes by applying the plan created in step 5
    ```bash
    terraform apply -var-file="env_vars/<env>.tfvars"
    ```
    > use `-lock=false` to disable locking temporarily

## Statefile with backend s3 
 Create a `./backend` folder in each environment, add the s3 backend config scripts and deploy terraform backend. The following will initiate terraform backend on the new environment. This step will create backend with s3
    ```bash
    terraform init
    terraform plan --out=output-backend.tfplan
    terraform apply output-backend.tfplan
    ```


## Managing terraform variables and secrets
For vaiables create variables.tf and store all the env related variables to file. Link the secrets by creating <env>.tfvars and <env>.auto.tfvars files add all the secrets to <env>.auto.tfvars which will auto apply while creating infrastructure.   
```bash
    terraform plan -var-file="<env>.tfvars"
    terraform apply -var-file="<env>.tfvars"
```

