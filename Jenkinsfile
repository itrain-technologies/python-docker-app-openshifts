node{
   
   stage("App Build started"){
      echo 'App build started..'
      git credentialsId: 'Github-ID', url: 'https://github.com/itrain-technologies/python-docker-app-openshifts.git'
      }
   
   stage('Docker Build') {
     def app = docker.build "aashishprabhakaran/itrain-technologies"
    }
   
   stage("Tag & Push image"){
      withDockerRegistry([credentialsId: 'dockerID',url: ""]) {
          sh 'docker tag aashishprabhakaran/itrain-technologies aashishprabhakaran/itrain-technologies:dev'
          sh 'docker push aashishprabhakaran/itrain-technologies:dev'
          sh 'docker push aashishprabhakaran/itrain-technologies:latest'
      }
    }
   
   stage("App deployment started"){
     sh 'oc login --token=SyC6k2uOVRfPWorLjeFCNV8ygtEgoF80HQ1laz3po_I --server=https://api.us-east-1.online-starter.openshift.com:6443'
     //sh 'oc new project python app'
     sh 'oc new-app aashishprabhakaran/python-app:python-1.0 --name python-app'
     sh 'oc expose svc python-app --name=python-app'
     sh 'oc status'
    }
   
    stage('App deployed to Openshift environment') {
     echo 'App deployed to Openshift environment..'
    }
   
}
