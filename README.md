# rhoai-maas

This pattern is an implementation of [the Models-as-a-Service docs](https://docs.redhat.com/en/documentation/red_hat_openshift_ai_self-managed/3.3/html/govern_llm_access_with_models-as-a-service/index).

There looks to be a similar implementation in [Introducing Models-as-a-Service in OpenShift AI](https://developers.redhat.com/articles/2025/11/25/introducing-models-service-openshift-ai#what_is_models_as_a_service__maas__),
which is also used as a reference.

## Installation of this pattern

1. Fork/clone this repo
2. Log into an OpenShift Cluster of version `4.19.9` or later
3. `cd` into the directory you cloned this repo into
4. Run `./pattern.sh make install`

## Testing model

```bash
MODEL_ADDRESS=$(oc get gateway -n openshift-ingress maas-default-gateway -o jsonpath='{.spec.listeners[0].hostname}')
MAAS_ENDPOINT="https://$MODEL_ADDRESS/rhoai-maas-prod/granite-4-premium"
COMPLETIONS_ENDPOINT="$MAAS_ENDPOINT/v1/chat/completions"
TOKEN=$(oc whoami -t)

curl -kv "$COMPLETIONS_ENDPOINT" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $TOKEN" \
  -d '{
    "messages": [{"role": "user", "content": "Hi"}],
    "max_tokens": "10"
  }'
```
