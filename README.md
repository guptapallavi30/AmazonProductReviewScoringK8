# AmazonProductReviewScoringK8
AmazonProductReviewScoring flask app configured with kubernetes instead of docker

------
Apply secret and configmap files first. We need the authentication before using our variables in the deployment/service configuration files.
    kubectl apply -f [filename.yaml]

now, we deploy backend services/deployments (mongo.yaml, mongo-express.yaml)

Start the service
    minicube service mongo-express-service

------

Create configmap with environment variables

Create a config map with dynamic enviornmentt variables
    kubectl create configmap flask-app2-configmap \
    --from-literal=local_model_files_path=$PWD \
    --from-literal=volume_files_path=/app/model_files \
    --from-literal=model_xz_file=compressed_amazon_fashion_overall_score_generator_model_3.xz \
    --from-literal=tfidf_file=tfidf_vectorizer_3.pkl \
    --from-literal=tfidf_zip=tfidf_vectorizer_3.pkl.zip

After creating the file, we have to make it executable:
    chmod +x create-configmap.sh

Finally, wee can rrun the config creation file
    s./create-configmap.sh

see the created configmap
kubectl get configmap flask-app-configmap -o yaml
kubectl get configmap flask-app-configmap -o json
------
Run flask app GIVEN precreated image

docker run -v ${PWD}/model_files:/app/model_files -p 8000:5000 model_app_k8:v1.0.0

dockerhub image name:
guptapallavi30/model_app_k8:v1.0.0


tag image
docker tag model_app_k8:v1.0.1 guptapallavi30/model_app_k8:v1.0.1

puush image
docker push guptapallavi30/model_app_k8:v1.0.0

add image to .yaml file
guptapallavi30/model_app_k8:v1.0.0
    

interactive terminal
kubectl exec -it <pod-name> -- /bin/bash

 docker tag docker-volume-minikube-example:latest guptapallavi30/docker-volume-minikube-example:latest


 apply pvc file
 apply deployment file + service file
 minikube service <service-name> --url