node {
    def server = Artifactory.server 'Artifactory-Kruttik-Local'
    def rtGradle = Artifactory.newGradleBuild()

    stage 'Build'
        checkout scm

    stage 'Artifactory configuration'
        rtGradle.deployer repo:'libs-snapshot-local', server: server
        rtGradle.resolver repo:'remote-repos', server: server
        rtGradle.useWrapper = true

    stage 'Exec Gradle'
        def buildInfo = rtGradle.run rootDir: "./", buildFile: 'build.gradle', tasks: 'clean build artifactoryPublish'

    stage 'Publish build info'
        server.publishBuildInfo buildInfo
}