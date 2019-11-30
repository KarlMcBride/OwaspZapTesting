// Source: https://wiki.jenkins.io/display/JENKINS/ZAP+Pipeline+Plugin

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
                    startZap(host: "localhost", port: 5555, timeout:5, zapHome: "/opt/zaproxy", sessionPath:"vulnweb_demo.session", allowedHosts:['localhost'])
                }
            }
        }
        //stage('Build & Test')
        //{
        //    steps
        //    {
        //        script
        //        {
        //            sh "mvn verify -Dhttp.proxyHost=127.0.0.1 -Dhttp.proxyPort=9091 -Dhttps.proxyHost=127.0.0.1 -Dhttps.proxyPort=9091" // Proxy tests through ZAP
        //        }
        //    }
        //}
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