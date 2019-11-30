pipeline
{
    agent { label 'buildnode' }
    stages
    {
        stage('Initialise ZAP')
        {
            steps
            {
                startZap(host: "localhost", port: 5555, timeout: 900, zapHome: "/opt/jenkinsRemotingWorkspace/tools/com.cloudbees.jenkins.plugins.customtools.CustomTool/ZAP_2_8_1/ZAP_2_8_1",
                allowedHosts:['localhost'], sessionPath:"/path/to/session.session")
            }
        }
        stage('Build & Test')
        {
            steps
            {
                script
                {
                     // Proxy tests through ZAP
                    //sh "mvn verify -Dhttp.proxyHost=127.0.0.1 -Dhttp.proxyPort=9091 -Dhttps.proxyHost=127.0.0.1 -Dhttps.proxyPort=9091"
                    runZapCrawler(host: "http://testphp.vulnweb.com")
                }
            }
        }
    }
    post
    {
        always
        {
            script
            {
                archiveZap(failAllAlerts: 1, failHighAlerts: 0, failMediumAlerts: 0, failLowAlerts: 0, falsePositivesFilePath: "zapFalsePositives.json")
            }
        }
    }
}