# CI-CD-Pipeline-Implementation-using-git-codeBuild-codeDeploy-code-pipeline-S3-and-IAM.

FULL CI/CD FLOW
Developer Pushes Code
        |
        v
GitHub Repository
        |
        v
Webhook Trigger
        |
        v
CodePipeline Starts
        |
        v
Source Artifact Created
        |
        v
Stored in S3
        |
        v
CodeBuild Triggered
        |
        v
Temporary Build Container Created
        |
        v
buildspec.yml Executed
        |
        v
Build Artifact Generated
        |
        v
Stored in S3
        |
        v
CodeDeploy Triggered
        |
        v
Deployment Group Identifies EC2
        |
        v
CodeDeploy Agent Downloads Artifact
        |
        v
appspec.yml Executed
        |
        v
Lifecycle Hooks Run
        |
        v
Node.js Application Started
