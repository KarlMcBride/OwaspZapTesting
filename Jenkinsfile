// Source: https://wiki.jenkins.io/display/JENKINS/ZAP+Pipeline+Plugin

pipeline
{
    agent { label "buildnode" }
    stages
    {
        stage('Start ZAP')
        {
            steps
            {
                // Start ZAP at /opt/zaproxy/zap.sh, allowing scans on github.com (if allowedHosts is not provided, any local addresses will be used
                sh '/opt/jenkinsRemotingWorkspace/tools/com.cloudbees.jenkins.plugins.customtools.CustomTool/ZAP_w2019-11-25/ZAP_D-2019-11-25/zap.sh -daemon -host localhost -port 5555 -cong api.disablekey=true -config api.addrs.addr.regex=true -config api.addrs.addr.name=.* -config connection.timeoutInSecs=300'
            }
        }
        stage('Build & Test')
        {
            steps
            {
                runZapCrawler(host: "http://testphp.vulnweb.com")
            }
        }
    }
    //post
    //{
    //    always
    //    {
    //        script
    //        {
    //            archiveZap(failAllAlerts: 1, failHighAlerts: 0, failMediumAlerts: 0, failLowAlerts: 0, falsePositivesFilePath: "zapFalsePositives.json")
    //        }
    //    }
    //}
}