# kiwi-blog-0001-cdk-force-tagging

This example shows how to create a custom synthesizer, to forcefully populate the tags of the deployed stacks and relative resources.

You can find the relative blog post at: https://blog.infra.kiwi/aws-cdk-force-tagging-all-stacks-with-a-git-repository-name-ee30ec7e6eae

## Important files

* CDK entrypoint: [bin/app.ts](bin/app.ts)
* Synthesizer definition and wrapper function: [lib/synthesizer.ts](lib/synthesizer.ts)
* Example stack: [lib/stack.ts](lib/stack.ts)

## Usage

Run:

```shell
npm install
npm run cdk:deploy:all
```

Verify the execution with

```shell
aws cloudformation describe-stacks --stack-name kiwi-blog-0001-cdk-force-tagging --query 'Stacks[*].[StackName,Tags]' 
```

Which should print

```json
[                                                                                             
    [
        "kiwi-blog-0001-cdk-force-tagging",
        [
            {
                "Key": "Repository",
                "Value": "infrakiwi/kiwi-blog"
            }
        ]
    ]
]
```

Then, you can destroy the deployed infrastructure with:

```shell
npm run cdk:destroy:all
```

## Useful commands

### CDK commands

```shell
# Performs a CDK diff against the current deployed environment
npm run cdk:diff

# Runs the CDK deployment
npm run cdk:deploy:all

# Destroys all the CDK deployment resources
npm run cdk:destroy:all

# Shows the synthesized CloudFormation template
npm run cdk:synth
```

### JS commands

```shell
# Run tests
npm run test

# Run lint
npm run lint
```