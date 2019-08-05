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
     sh 'oc new-app aashishprabhakaran/python-app:1.0 --name python-app'
     sh 'oc expose svc python-app --name=python-app'
     sh 'oc status'
    }
   
    stage('App deployed to Openshift environment') {
     echo 'App deployed to Openshift environment..'
    }
   
//sh 'oc import-image manee2k6/python-app:pattabhi-1.0 --name python-app'
   //sh 'oc login --token=SyC6k2uOVRfPWorLjeFCNV8ygtEgoF80HQ1laz3po_I --server=https://api.us-east-1.online-starter.openshift.com:6443'
   //sh 'oc login --token=U0mNHuUe1VMJNXU7UplhPs46ywPnq6FGfz0cMlQcSuQ --server=https://api.us-east-2.online-starter.openshift.com:6443'

//openshift
//oc login --token=OXcg8B_XN82LvMDkNCc9uGG-zA0YzIb-UYulztK2jZ8 --server=https://api.us-east-1.online-starter.openshift.com:6443


}
