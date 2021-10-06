# Build source

```
export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
cd src
./mvnw clean package -Dmaven.test.skip=true
cd ..
```

# Build containers

```
cd src/apache
docker build -t gcr.io/pl-dev-infra/demos/microservice-kafka/apache:1.0 .
cd ../..

cd src/microservice-kafka-invoicing
docker build -t gcr.io/pl-dev-infra/demos/microservice-kafka/invoicing:1.0 .
cd ../..

cd src/microservice-kafka-load-test
docker build -t gcr.io/pl-dev-infra/demos/microservice-kafka/load-test:4.0 .
cd ../..

cd src/microservice-kafka-order
docker build -t gcr.io/pl-dev-infra/demos/microservice-kafka/order:1.0 .
cd ../..

cd src/microservice-kafka-shipping
docker build -t gcr.io/pl-dev-infra/demos/microservice-kafka/shipping .
cd ../..

cd src/postgres
docker build -t gcr.io/pl-dev-infra/demos/microservice-kafka/postgres .
cd ../..
```

# Push containers

```
docker push gcr.io/pl-dev-infra/demos/microservice-kafka/apache:1.0
docker push gcr.io/pl-dev-infra/demos/microservice-kafka/invoicing:1.0
docker push gcr.io/pl-dev-infra/demos/microservice-kafka/load-test:4.0
docker push gcr.io/pl-dev-infra/demos/microservice-kafka/order:1.0
docker push gcr.io/pl-dev-infra/demos/microservice-kafka/shipping:1.0
docker push gcr.io/pl-dev-infra/demos/microservice-kafka/postgres:1.0
```

# Deploy

To run the demo app:

```
kubectl create namespace kafka-demo
cd kubernetes
kubectl apply -f . -n kafka-demo
kubectl get services -n kafka-demo
cd ..
```

It may take a few minutes for the demo to fully spin up, and some pod restarts along the way are normal.

Visit the apache external IP (with port) to visit the site.
Visit the load-test's external IP (with port) to start a load test.
