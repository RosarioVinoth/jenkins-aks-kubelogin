pipeline {
  environment {
	MY_KUBECONFIG = credentials('kube.poc1')
  }
  agent any
  stages {
    stage('Pre-clean') {
		steps{
		
			sh """
				rm -rf *
			"""
		}
    }
    stage('Connect to AKS'){
      steps{
          withCredentials([azureServicePrincipal('57b1e02e-cc79-4a33-8c8f-7124a5c88b57')]) {
		    sh """
				wget https://github.com/Azure/kubelogin/releases/download/v0.0.9/kubelogin-linux-amd64.zip
				unzip kubelogin-linux-amd64.zip
				export PATH=bin/linux_amd64:$PATH
				
				
				export KUBECONFIG=$MY_KUBECONFIG
				cat $MY_KUBECONFIG > kubeconfig
				export KUBECONFIG=kubeconfig
				kubelogin convert-kubeconfig -l spn
				
				export AAD_SERVICE_PRINCIPAL_CLIENT_ID="\$AZURE_CLIENT_ID"
				export AAD_SERVICE_PRINCIPAL_CLIENT_SECRET="\$AZURE_CLIENT_SECRET"
				
				kubectl create namespace sampleapp --dry-run=client -o yaml | kubectl apply -f -
				kubectl get ns
				kubectl apply -n sampleapp -f sample-internal-app.yaml
			"""
		
      }
    }
  }
  }
}
