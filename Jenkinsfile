pipeline
{
    agent any
    stages
    {
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