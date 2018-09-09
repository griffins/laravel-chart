# laravel-chart
Helm Chart For Laravel Deployment

I wanted simple chart that i can use to deploy any laravel application. I wanted something that supports queues, scheduled jobs and the web application service.

This chart so far supports only the web app. I have plans to support scheduled jobs and queue in no time. 

Example of how i use it on my gitlab devops scripts

```
helm upgrade --install \
      --wait \
      --set service.enabled="$service_enabled" \
      --set releaseOverride="$CI_ENVIRONMENT_SLUG" \
      --set image.repository="$CI_APPLICATION_REPOSITORY" \
      --set image.tag="$CI_APPLICATION_TAG" \
      --set image.pullPolicy=IfNotPresent \
      --set image.secrets[0].name="$secret_name" \
      --set application.track="$track" \
      --set application.configMap="$STAGING_CONFIG" \
      --set service.url="$CI_ENVIRONMENT_URL" \
      --set service.internalPort="80" \
      --set replicaCount="$replicas" \
      --namespace="$KUBE_NAMESPACE" \
      --version="$CI_PIPELINE_ID-$CI_JOB_ID" \
      "$name" \
      chart/
  ```
