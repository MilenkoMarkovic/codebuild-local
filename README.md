# aws-codebuild-local-build-demo
Learn how to run builds on a local computer using the CodeBuild Agent and Docker. This is incredibly useful to test the buildspec.yml file before implementing it in the build project on AWS CodeBuild. 🚀


# CodeBuild Local Setup Guide 🚀

This guide outlines the steps to set up CodeBuild locally on your machine. With this local setup, you can build and test projects using the CodeBuild environment.

## Prerequisites 📋

Before you begin, make sure you have the following installed on your system:

- Docker: [Download Docker](https://www.docker.com/get-started)
- Git: [Download Git](https://git-scm.com/downloads)

## Step 1: Setup the CodeBuild Image 🛠️

Clone the CodeBuild image repository:
```sh
git clone https://github.com/aws/aws-codebuild-docker-images.git
```

Navigate to the cloned directory:
```sh
cd aws-codebuild-docker-images/ubuntu/standard/5.0
```

Build the CodeBuild image (This might take some time):
```sh
docker build -t aws/codebuild/standard:5.0 .
```

## Step 2: Download the CodeBuild Agent 📥

Download the CodeBuild agent:
- For x86_64 version:
  ```sh
  docker pull public.ecr.aws/codebuild/local-builds:latest
  ```
- For ARM version:
  ```sh
  docker pull public.ecr.aws/codebuild/local-builds:aarch64
  ```

## Step 3: Demo Building A Sample Java Project

Clone this sample Springboot Java project from GitHub. The project already has a `buildspec.yml` file that specifies the build commands and environment variables. You can modify this file to suit your project's requirements. It also has `codebuild_build.sh` script that runs the CodeBuild Agent to build the project. You can skip Step 4 and directly run this script to build the project. But if you want to learn how to run the CodeBuild Agent, follow Step 4.

```sh
git clone https://github.com/hsiddhu2/aws-codebuild-local-build-demo.git
``` 

## Step 4: Run the CodeBuild Agent to Build a Project 🏗️

NOTE: This step is optional if you have used the sample project from Step 3. In case you want to build your own project then download the `codebuild_build.sh` script from the sample project and follow the steps below.

To run the CodeBuild Agent, navigate to the root directory of your project.

Download the `codebuild_build.sh` script:
```sh
curl -O https://raw.githubusercontent.com/aws/aws-codebuild-docker-images/master/local_builds/codebuild_build.sh
chmod +x codebuild_build.sh
```

Run the script with the following command, specifying the container image created in Step 1 (`aws/codebuild/standard:5.0`) and the artifact directory path:
```sh
./codebuild_build.sh -i aws/codebuild/standard:5.0 -a artifacts_directory -s /path/to/source/directory -e .env -c
```
Where:
- `-i`: Specifies the code build container image.
- `-a`: Specifies the artifact directory.
- `-s`: Specifies the source directory (default is the current directory).
- `-e`: Specifies the environment variable file path.
- `-c`: Specifies the AWS configure file and credentials from your local host. This includes `~/.aws` and `AWS_*` environment variables.
- `-b`: Specifies `buildspec.yml` file to override the default (file in the current directory).


## Conclusion 🎉

You've successfully set up CodeBuild locally! This setup allows you to replicate the CodeBuild environment on your machine for building and testing projects efficiently.

Feel free to customize the provided commands and paths according to your project's requirements.

Happy building! 🚀

# codebuild-local
