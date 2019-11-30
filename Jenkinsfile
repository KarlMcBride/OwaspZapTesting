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
                startZap(host: "192.168.1.166", port: 5557, timeout:500, zapHome: "/opt/jenkinsRemotingWorkspace/tools/com.cloudbees.jenkins.plugins.customtools.CustomTool/ZAP_w2019-11-25/ZAP_D-2019-11-25", sessionPath:"session.session", allowedHosts:['192.168.1.166'])
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