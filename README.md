# Official Rest API of api.royalflushnetwork.com

> Uses Rust for backend code and AWS for Infrastructure

## Pre-requisite
1. [AWS getting started](https://docs.aws.amazon.com/sdk-for-rust/latest/dg/getting-started.html)
2. [Cargo Lambda Getting Started](https://www.cargo-lambda.info/guide/getting-started.html)

- Creating new Endpoint

```sh
cargo lambda new
```

- Local Dev / Testing

```sh
cargo lambda watch
```

- Test your function

```sh
cargo lambda invoke --data-ascii "{ \"command\": \"hi\" }"
```

> If your function integrates with Amazon API Gateway, you can use one of the payload examples that we provide by using the --data-example flag

```sh
cargo lambda invoke http-lambda --data-example apigw-request
```

- Build for release

```sh
cargo lambda build --release --arm64
```

- Deploy on AWS

> If you run this command without any flags, Cargo Lambda will try to create an execution role with Lambda's default service role policy AWSLambdaBasicExecutionRole.

```sh
cargo lambda deploy --iam-role FULL_ROLL_ARN FUNCTION_NAME
```

- ENV Variables (.env) file

```rs
cargo lambda deploy --env-file .env http-lambda
```

- Deploy Configuration in Cargo's metadata

```toml
[package.metadata.lambda.deploy]
memory = 512                   # Function's memory
timeout = 60                   # Function's execution timeout
tracing = "active"             # Tracing mode
role = "role-full-arn"         # Function's execution role
env_file = ".env.production"   # File to load environment variables from
env = { "VAR1" = "VAL1" }      # Additional environment variables
layers = [                     # List of layers to deploy with your function
    "layer-full-arn"
]
tags = { "team" = "lambda" }   # List of AWS resource tags for this function
```

- Using with Existing Rust code (use init instea of new)
```sh
cargo lambda init --name init-project
```

- Generate a Github Workflow on the folder of newly created lambda function

> create `.github/workflows/rust.yml`

```sh
mkdir -p .github/workflows/rust.yml
```

 press <kbd>Alt|Opt</kbd> + <kbd>F2</kbd> select  `workflow`

 or simply type `workflow` on the new main.yml file to trigger snippet


