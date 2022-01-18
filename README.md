# hello-sam-app

SAM sample app with environment specific resources.
The intention is to have all environment specific params in the [samconfig.toml](samconfig.toml) file and then 
provide only the environment name for the sam cli:

```bash
sam build
sam deploy --config-env dev
# or
sam deploy --config-env prod
```

Problem:
Common settings like `stack_name="hello-sam-app"` are not picked up from the `[default.deploy.parameters]` section, 
and I don't want  to repeat them for all environments.

error message:
```bash
$ sam  deploy --config-env prod
Usage: sam deploy [OPTIONS]
Try 'sam deploy -h' for help.

Error: Missing option '--stack-name', 'sam deploy --guided' can be used to provide and save needed parameters for future deploys.

$ sam --version
SAM CLI, version 1.37.0
```

relevant samconfig content:
```toml
[default.deploy]
[default.deploy.parameters]
stack_name="hello-sam-app"
```