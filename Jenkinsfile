node {
    def server = Artifactory.server 'Artifactory-Kruttik-Local'
    def rtGradle = Artifactory.newGradleBuild()

    stage 'Build'
        checkout scm

    stage 'Artifactory configuration'
        rtGradle.tool = GRADLE_TOOL // Tool name from Jenkins configuration
        rtGradle.deployer repo:'gradle-dev-local', server: server
        rtGradle.resolver repo:'remote-repos', server: server
        rtGradle.useWrapper = true

    stage 'Exec Gradle'
        def buildInfo = rtGradle.run rootDir: "./", buildFile: 'build.gradle', tasks: 'clean artifactoryPublish'

    stage 'Publish build info'
        server.publishBuildInfo buildInfo
}