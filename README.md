setup/install jenkins

Make a freestyle project

![create a new project](./jenkins-freestyle-project.PNG)

Setup source code management (link to git and chose branch)

![setup git](./jenkins-source-code-management.PNG)

Build script (workspace is now the chosen git)

![build script](./jenkins-build.PNG)

deployment script
`
#!/bin/bash
IMAGE_NAME=$1
SERVICE_NAME=$2

docker pull mikkeldjurhuus/${IMAGE_NAME}:latest
docker-compose up -d --no-deps --build ${SERVICE_NAME}
docker image prune -a
`

