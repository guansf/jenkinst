#!groovy

@Library('jenkinst') _

def tools = new org.devops.tools()



String workspace = "/opt/jenkins/workspace"

//Pipeline
pipeline {
    agent  any
    

    options {
        timestamps()  //日志会有时间
        skipDefaultCheckout()  //删除隐式checkout scm语句
        disableConcurrentBuilds() //禁止并行
        timeout(time: 1, unit: 'HOURS')  //流水线超时设置1h
    }

    stages {
        //下载代码
        stage("GetCode"){ //阶段名称
            when { environment name: 'test', value: 'abcd' }
            steps{  //步骤
                timeout(time:5, unit:"MINUTES"){   //步骤超时时间
                    script{ //填写运行代码
                        println('获取代码')
                        println("${test}")
                        
                        
                    }
                }
            }
        }

        stage("01"){
            failFast true
            parallel {
        
                //构建
                stage("Build"){
                    steps{
                        timeout(time:20, unit:"MINUTES"){
                            script{
                                println('应用打包')
                                

                            }
                        }
                    }
                }
        
                //代码扫描
                stage("CodeScan"){
                    steps{
                        timeout(time:30, unit:"MINUTES"){
                            script{
                                print("代码扫描")

                                tools.PrintMsg("this is my lib!")
                                      
                            }
                        }
                    }
                }
            }
        }
    }

    //构建后操作
    post {
        always {
            script{
                println("always")
            }
        }

        success {
            script{
                currentBuild.description = "\n 构建成功!" 
            }
        }

        failure {
            script{
                currentBuild.description = "\n 构建失败!" 
            }
        }

        aborted {
            script{
                currentBuild.description = "\n 构建取消!" 
            }
        }
    }
}
