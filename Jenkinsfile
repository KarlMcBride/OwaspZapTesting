pipeline
{
    agent any
    stages
    {
        stage('Setup')
        {
            steps
            {
                script
                {
                    // Start ZAP at /opt/zaproxy/zap.sh, allowing scans on github.com (if allowedHosts is not provided, any local addresses will be used
                    //startZap(host: "127.0.0.1", port: 9091, timeout:500, zapHome: "/opt/zaproxy", sessionPath:"/somewhere/session.session", allowedHosts:['github.com']) }
                }
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