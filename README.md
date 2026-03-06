# rhoai-maas

This pattern is an implementation of [the Models-as-a-Service docs](https://docs.redhat.com/en/documentation/red_hat_openshift_ai_self-managed/3.3/html/govern_llm_access_with_models-as-a-service/index).

## Needs to be fixed

1. The `kuadrant-operator-controller-manager-*` in `openshift-operators` needs to be deleted in order for the Kuadrant resource to be marked as Ready
