# ------------------------------------
# The following variables should not be changed except for advanced use cases

root ?= $(shell pwd)/..

namespace ?= camunda

.PHONY: all
all: install-keycloak

# 1 install keycloak (and corresponding postgres db)
.PHONY: install-keycloak
install-keycloak:
	-kubectl create namespace $(namespace)
	-kubectl config set-context --current --namespace=$(namespace)
	-kubectl apply -f $(root)/keycloak/camunda-platform/charts/identity/charts/keycloak/charts/postgresql/templates/ -n $(namespace)
	-kubectl apply -f $(root)/keycloak/camunda-platform/charts/identity/charts/keycloak/charts/postgresql/templates/primary/ -n $(namespace)
	-kubectl apply -f $(root)/keycloak/camunda-platform/charts/identity/charts/keycloak/templates/ -n $(namespace)
	-kubectl apply -f $(root)/keycloak/camunda-platform/templates/ -n $(namespace)

.PHONY: clean-keycloak
clean-keycloak:
	# -kubectl delete -n $(namespace) pvc -l app.kubernetes.io/instance=$(release)
	# -kubectl delete -n $(namespace) pvc -l app=elasticsearch-master
	-kubectl delete namespace $(namespace)

include $(root)/include/camunda.mk
