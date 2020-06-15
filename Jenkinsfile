pipeline {
  agent any
  stages {
    stage('clone codes') {
      steps {
        git(url: 'https://github.com/XiufanJi/hello_world.git', branch: 'master')
      }
    }

    stage('test') {
      steps {
        sh '''#!/bin/bash
echo "begin test!"
mvn package'''
      }
    }

    stage('package') {
      steps {
        archiveArtifacts 'target/*.jar'
      }
    }

    stage('run packge') {
      steps {
        sh '''
	#!/bin/bash
echo "===copy file from container to local system==="
echo -e "\n"
# 判断命令是否执行成功
# 每条命令执行后都有一个返回值，该值使用？表示，一般执行成功后返回为0
if test -d /home/buildartifacts
then
	cd /home/buildartifacts
	parentdir='hello_world_master'
	
	if test -d ./${parentdir}
	then
		echo "the target directory already exists"
	else
		echo "No such directory, create one"
		mkdir $parentdir
	fi

	cd $parentdir
	childdir=`date +%Y%m%d`
	if test -d ./${childdir}
	then
		echo "the target directory already exists"
	else
		echo "No such directory, create one"
		mkdir `date +%Y%m%d`
	fi
	if [ $? -eq 0]; then cd $childdir; fi
	cp -r /var/jenkins_home/workspace/hello_world_master/target/CITest-1.0-SNAPSHOT.jar .
	if [$? -eq 0]
	then 
	    echo "===begin running file==="
	    echo -e "\n"
	    java -jar CITest-1.0-SNAPSHOT.jar
	    echo -e "\n"
	    echo "===complete!==="
	else
	    echo "copy file failed!"
	fi
else
	echo "No such directory"
fi
	'''
      }
    }

  }
}
