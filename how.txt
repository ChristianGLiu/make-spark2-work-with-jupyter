# make-spark2-work-with-jupyter

Build steps -

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
