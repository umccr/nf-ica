# nf-ica

## Development

This section covers how pipeline developers can iterate locally on draft workflows using the ICAv2 development project.

### Prerequisites

- Access to the AWS secret containing the ICAv2 access token
- The `icav2` CLI installed and configured

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
   icav2 projects enter development
   icav2 projectpipelines update <updated_pipeline_repo_zipped> <pipeline_id>
   ```

   - `<updated_pipeline_repo_zipped>` — path to the zipped pipeline repository with your local changes.
   - `<pipeline_id>` — the ID of the pipeline to update (found in `config/ica_pipelines.yaml`).
