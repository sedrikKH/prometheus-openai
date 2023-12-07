# prometheus-openai

## Action sequence

## Install krew
```
(   set -x; cd "$(mktemp -d)" &&   OS="$(uname | tr '[:upper:]' '[:lower:]')" &&   ARCH="$(uname -m | sed -e 's/x86_64/amd64/' -e 's/\(arm\)\(64\)\?.*/\1\2/' -e 's/aarch64$/arm64/')" &&   KREW="krew-${OS}_${ARCH}" &&   curl -fsSLO "https://github.com/kubernetes-sigs/krew/releases/latest/download/${KREW}.tar.gz" &&   tar zxvf "${KREW}.tar.gz" &&   ./"${KREW}" install krew; )
```
## Install plugin
```
kubectl krew index add kubectl-ai https://github.com/sozercan/kubectl-ai
kubectl krew install kubectl-ai/kubectl-ai
``` 

## Setting up alias and ENV

```
alias k=kubectl
read -s OPENAI_API_KEY
export OPENAI_API_KEY=$OPENAI_API_KEY
```

## Create promt requests
We'll use additional flags for plugin:
* **--require-confirmation=false**  - this can be set to prompt the user for confirmation before applying the manifest
* **--raw** - output only clear code

## Example:

```
k kubectl-ai "Create Application pod Config" --require-confirmation=false --raw > app.yaml
```


| NAME                    | PROMPT                                         | DESCRIPTION                                                                                     | EXAMPLE                                                                                                                            |
|-------------------------|------------------------------------------------|-------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|
| app.yaml                | Create Application pod Config                  |         Defines a pod with a container image, resource   requirements, and other details.       | <a   href='https://github.com/sedrikKH/prometheus-openai/blob/main/yaml-files/app.yaml'>app.yaml</a>                               |
| app-livenessProbe.yaml  | Create liveness Probe config                   |         Monitors the health of a container and restarts it if   it becomes unresponsive.        | <a   href='https://github.com/sedrikKH/prometheus-openai/blob/main/yaml-files/app-livenessProbe.yaml'>app-livenessProbe.yaml</a>   |
| app-readinessProbe.yaml | Create readiness Probe config                  |         Monitors the readiness of a container to receive   traffic.                             | <a   href='https://github.com/sedrikKH/prometheus-openai/blob/main/yaml-files/app-readinessProbe.yaml'>app-readinessProbe.yaml</a> |
| app-volumeMounts.yaml   | Creat volume mounts config                     |         Allows a container to access persistent data stored   in volumes.                       | <a   href='https://github.com/sedrikKH/prometheus-openai/blob/main/yaml-files/app-volumeMounts.yaml'>app-volumeMounts.yaml</a>     |
| app-cronjob.yaml        | Create cron job                                |         Schedules a job to run at specified times or   intervals.                               | <a   href='https://github.com/sedrikKH/prometheus-openai/blob/main/yaml-files/app-cronjob.yaml'>app-cronjob.yaml</a>               |
| app-job.yaml            | Create job config yaml                         |         Defines a batch job that runs to completion.                                            | <a   href='https://github.com/sedrikKH/prometheus-openai/blob/main/yaml-files/app-job.yaml'>app-job.yaml</a>                       |
| app-multicontainer.yaml | Create multicontainer appplication config yaml |         Defines a pod with multiple containers.                                                 | <a   href='https://github.com/sedrikKH/prometheus-openai/blob/main/yaml-files/app-multicontainer.yaml'>app-multicontainer.yaml</a> |
| app-resources.yaml      | Create resource usage config yaml              |         Defines resource limits and requests for a container.                                   | <a   href='https://github.com/sedrikKH/prometheus-openai/blob/main/yaml-files/app-resources.yaml'>app-resources.yaml</a>           |
| app-secret-env.yaml     | setup secret as ENV                            |         Sets up a Kubernetes Secret as an environment   variable for a container.               | <a   href='https://github.com/sedrikKH/prometheus-openai/blob/main/yaml-files/app-livenessProbe.yaml'>app-secret-env.yaml</a>      |