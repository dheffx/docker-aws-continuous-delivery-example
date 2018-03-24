# docker aws continuous delivery example

boilerplate cloudformation template and codebuild buildspec for docker image continuous delivery using aws devtools

creates a codecommit repo, a codebuild project, a codepipeline pipeline, an ecr, and the supporting s3 buckets and iam roles/policies

out of the box you will have a set up so any commit to the master of the codecommit repo
will build your image, and push it to ecr with a set of tags

## Set up
### create the stack

```
export LIBRARY_NAME=example
export IMAGE_NAME=myapp
./scripts/create
```

### set repo to codecommit
```
REPO_URL=$(aws cloudformation describe-stacks --stack-name $LIBRARY_NAME-$IMAGE_NAME-stack | jq -r ".Stacks[0].Outputs[1].OutputValue")
git remote set-url origin $REPO_URL
```

### drop in your dockerfile
replace the example Dockerfile with your own, add/commit/push it

## xx
this was meant to be a quick example
if this were built out further, would maybe work on adding
 - default life cycle policies
 - out-of-the-box kms signing of images
