
cluster:
	gcloud container --project "dataminer-test" clusters create "main-test" --zone "us-east1-c" \
	--cluster-version "1.8.7-gke.1" --machine-type "g1-small" --image-type "COS" --disk-size "15" \
	--num-nodes "2" --enable-cloud-logging --enable-cloud-monitoring \
	--no-enable-legacy-authorization

update:
	kubectl apply -f .

curl:
	curl IP -H 'Host: helloworld-v1.example.com'
	curl IP -H 'Host: helloworld-v2.example.com'


clean:
	kubectl delete -f .
	gcloud container clusters delete main --quiet
