# deploy-cdk-go

GitHub Actions simplifies deployment of Golang AWS CDK application to AWS account.

## Usage

See [Serverless Blueprint for Golang](https://github.com/fogfish/blueprint-serverless-golang) for complete set of examples 


Deploy GitHub Releases

```yaml
name: carry
on:
  release:
    types: [published]

jobs:
  it:
    strategy:
      matrix:
        stack:
          - blueprint-golang

    runs-on: ubuntu-latest
    steps:

      - uses: actions/checkout@v2

      - uses: fogfish/spawner-cdk@main
        with:
          go-version: 1.18
          stack: ${{ matrix.stack }}
          version: ${{ github.event.release.name }}
          issue-to-create: ./.github/issue-spawn-release.md
          aws-access-key: ${{ secrets.AWS_ACCESS_KEY }}
          aws-secret-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: eu-west-1

```

