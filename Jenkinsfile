timestamps {

node () {

	stage ('Spark Exercises - Checkout') {
 	 checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '', url: 'https://github.com/jpaulorio/spark-training.git']]])
	}
	stage ('Spark Exercises - Build') {

    def job = Jenkins.getInstance().getItemByFullName(${JOB_BASE_NAME}, Job.class)
    def build = job.getBuildByNumber(env.BUILD_ID as int)
    def userId = build.getCause(Cause.UserIdCause).getUserId()

    sh """
    sbt assembly
     """
        }
        stage('Spark Exercises - Publish') {
        s3Upload(consoleLogLevel: 'INFO', dontWaitForConcurrentBuildCompletion: false, entries: [[bucket: "com.thoughtworks.training.de.recife/$userId", excludedFile: '', flatten: true, gzipFiles: false, keepForever: false, managedArtifacts: false, noUploadOnFailure: true, selectedRegion: 'us-east-1', showDirectlyInBrowser: false, sourceFile: '**/target/scala-2.11/*.jar', storageClass: 'STANDARD', uploadFromSlave: false, useServerSideEncryption: false]], pluginFailureResultConstraint: 'FAILURE', profileName: 'AWS DE Trainining Recife', userMetadata: [])
        }
    }
}