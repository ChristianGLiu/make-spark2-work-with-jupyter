# make-spark2-work-with-jupyter

Build steps -

Install Spark
Create directory where spark directory is going to reside. Step into the directory

1
2
sudo mkdir /usr/apache
cd /usr/apache
Download Spark 2.0.0 from https://spark.apache.org/downloads.html

1
sudo wget http://d3kbcqa49mib13.cloudfront.net/spark-2.0.0-bin-hadoop2.7.tgz
Unpack the tar file

1
sudo tar -xvzf spark-2.0.0-bin-hadoop2.7.tgz
Remove the tar file after it has been unpacked

1
sudo rm spark-2.0.0-bin-hadoop2.7.tgz
Change the ownership of the folder and its elements

1
sudo chown -R spark:spark spark-2.0.0-bin-hadoop2.7
Update system variables

Step into the spark 2.0.0 directory and run pwd to get full path

1
2
cd spark-2.0.0-bin-hadoop2.7
pwd
Update the system environment file by adding SPARK_HOME and adding SPARK_HOME/bin to the PATH

1
sudo vi /etc/environment
export SPARK_HOME=/usr/apache/spark-2.0.0-bin-hadoop2.7

At the end of PATH add

${SPARK_HOME}/bin

Refresh the system environments

1
source /etc/environment


export SPARK_HOME=/Users/<path>/spark-2.1.0-hadoop2.7/
git clone https://github.com/apache/incubator-toree.git
cd incubator-toree
curl https://bintray.com/sbt/rpm/rpm | sudo tee /etc/yum.repos.d/bintray-sbt-rpm.repo
sudo yum install sbt
sbt compile
make clean release APACHE_SPARK_VERSION=2.1.0
pip install --upgrade ./dist/toree-pip/toree-0.2.0.dev1.tar.gz
pip freeze |grep toree 
jupyter toree install --spark_home=$SPARK_HOME

To Start the notebook

$ SPARK_OPTS='--master=local[4]' jupyter notebook

