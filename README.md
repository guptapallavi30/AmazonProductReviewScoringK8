# AmazonProductReviewScoringK8
AmazonProductReviewScoring flask app configured with kubernetes instead of docker

Apply secret and configmap files first. We need the authentication before using our variables in the deployment/service configuration files.
    kubectl apply -f [filename.yaml]

now, we deploy backend services/deployments (mongo.yaml, mongo-express.yaml)

Start the service
    minicube service mongo-express-service
    