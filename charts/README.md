## 1. Deployment
### 1.1. Flyte sandbox (locally)

#### 1.1.1. Install flytectl by shell script and set environment path**

    curl -sL https://ctl.flyte.org/install | bash
    export PATH=$HOME/bin:$PATH

#### 1.1.2. create cluster
* step 1. start flyte sandbox cluster 
 
      start sandbox by flytectl

* step 2: set env path for kube config and flytectl config 
    *Note: you can copy this variable in logs console after sandbox start.* 

       export KUBECONFIG=$KUBECONFIG:/<path_to>/.kube/config:/<path>/.flyte/k3s/k3s.yaml
       export FLYTECTL_CONFIG=/<path_to>/.flyte/config-sandbox.yaml

* Step 3: Open this url (http://localhost:30081/console) on your browser.**
### 1.2. Flyte Native (AWS)

#### 1.2.1. Deploy cluster 

Step 1: Follow [deployment flyte docs](https://docs.flyte.org/en/latest/deployment/aws/manual.html#deployment-aws-manual) to install some dependences

Step 2: Installing Flyte.

    export $FLYTE_HOME=<path-to-charts>
    helm install -n flyte -f $CHART_HOME/flyte-core/values-eks-native.yaml --create-namespace flyte $CHART_HOME/flyte-core/


Step 3: Install spark-operator:

    helm install -n spark-operator -f $CHART_HOME/spark-operator-chart/values.yaml spark-operator $CHART_HOME/spark-operator-chart --create-namespace

Step 4: Upgrade helm

    helm upgrade -n flyte -f $CHART_HOME/flyte-core/values-eks-native.yaml -f $CHART_HOME/flyte-core/values-override.yaml --create-namespace flyte $CHART_HOME/flyte-core/
