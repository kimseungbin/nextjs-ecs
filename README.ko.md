# 사전 준비

- [AWS CLI](https://formulae.brew.sh/formula/awscli)
- [AWS CLI configuration](https://docs.aws.amazon.com/cli/latest/reference/configure/)
    - `profile` 플래그를 사용하는 것을 권장합니다.
    - IAM 사용자는 템플릿에 정의된 모든 리소스를 생성, **업데이트 및 삭제**할 수 있는 권한이 있어야합니다.
    - IAM 사용자에게 [AWSCloudFormationFullAccess](https://docs.aws.amazon.com/aws-managed-policy/latest/reference/AWSCloudFormationFullAccess.html) 권한을 부여하세요.
- (Optional) [CloudFormation Lint](https://formulae.brew.sh/formula/cfn-lint)

# How to deploy

## Manual deployment

1. Run Lint
   ```Shell
    $ cfn-lint template.yaml
   ```
2. Deploy
    ```Shell
   $ aws cloudformation deploy --stack-name [STACK_NAME] --template-file [TEMPLATE_FILE_NAME] --capabilities CAPABILITY_IAM
   ```
    - `stack-name` flag is **required**.
    - `template-file` flag is **required**.
    - `capabilities` flag with CAPABILITY_IAM argument is required; it allows CloudFormation to create and update AWS IAM resource on behalf of the developer.
    - (optional) Use `parameters [file://path/to/template.yaml]` flag to override default parameters. 