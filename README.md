# nf-ica

Configurations and patches used to deploy nextflow pipelines onto ICAv2.

See [nf-ica-cli](https://github.com/umccr/nf-ica-cli) for commands to use to generation configurations and patches for this repo.

## Iterative Development

This section covers how pipeline developers can iterate locally on draft workflows, deployed via the nf-ica CLI using the ICAv2 development project.

### Prerequisites

- Access to the AWS secret containing the ICAv2 access token
- The `icav2` CLI installed and configured* 
- The `nf-ica` toolkit. 

*icav2 cli plugins required. I am in the process of updating this repo to be more user-friendly.

### Development Secret

The ICAv2 access token for the development project is stored in AWS Secrets Manager:

```
arn:aws:secretsmanager:ap-southeast-2:843407916570:secret:ICAv2JWTKey-umccr-prod-service-dev-95mZMB
```

### Updating a Pipeline

To iterate on a draft pipeline in the development project:

1. Retrieve the access token from the secret ARN above and export it:

   ```bash
   export ICAV2_ACCESS_TOKEN="<value_from_secret>"
   ```

2. Enter the development project and update the pipeline:

   ```bash
   export ICAV2_PROJECT_ID="<development_project_id>"
   icav2 projectpipelines update <updated_pipeline_repo_zipped> <pipeline_id>
   ```
   - `development_project_id` — the development project uuid
   - `<updated_pipeline_repo_zipped>` — path to the zipped pipeline repository with your local changes.
   - `<pipeline_id>` — the ID of the pipeline to update (found in `config/ica_pipelines.yaml`).
