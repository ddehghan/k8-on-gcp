# Set these environment variables

# DOMAIN_NAME = test.example.com
# PROJECT_ID = ABCD_1232

cluster0:
	gcloud compute addresses create static-ip-address-name --region="us-east1"


cluster1:
	gcloud container --project $(PROJECT_ID) clusters create "main" --zone "us-east1-c" \
	--cluster-version "1.8.7-gke.1" --machine-type "g1-small" --image-type "COS" --disk-size "15" \
	--num-nodes "2" --enable-cloud-logging --enable-cloud-monitoring \
	--no-enable-legacy-authorization


cluster2:
	helm init

	sleep 20

	kubectl create clusterrolebinding add-on-cluster-admin --clusterrole=cluster-admin --serviceaccount=kube-system:default

	sleep 10

	helm install --name cert-manager-helm stable/cert-manager \
	--set rbac.enabled=false

	sleep 20

	gcloud compute addresses list

	helm install --name nginx-ingress-helm stable/nginx-ingress \
	--set rbac.create=true \
	--set controller.service.loadBalancerIP="35.185.50.73"


cluster3:
	kubectl apply -f cert/
	kubectl apply -f .


cert-info:
	@echo "Get certificate info for: " $(DOMAIN_NAME)
	kubectl describe certificate $(DOMAIN_NAME)


update:
	kubectl apply -f .


curl:
	curl $(DOMAIN_NAME)
	curl --proto-default https $(DOMAIN_NAME)


clean:
	kubectl delete -f .
