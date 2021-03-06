##Objective

The Objective of this lab is to have the trucking demo up and running.

### Prerequsites:

<pre>
1) The setup scripts for the demo must be run from the Ambari machine. 
	- <b>For the lab please run it on sandbox.hortonworks.com. </b>

2) Demo will be installed and run under the <b>root</b> user.

3) Install wget
	$ yum -y install wget

4) Navigate to http://sandbox.hortonworks.com:8080 and check if HBase and Storm are up and running. If it is not running, please update it.

5) Turn off maintenace mode for HBase, Storm, Kafka, Falcon and Spark.

6) If running on sandbox:
	- Assign 8GB of RAM assigned to VM
	- Update the /etc/hosts file is correct with the host to ip address mapping.
</pre>	

- set JAVA_HOME, if not set.

<pre>

</pre>

## Instructions to install demo:
 -  Install git:
 	<pre>
 		yum -y install git
 	</pre>

<pre>
git clone https://github.com/shivajid/iot-truck-streaming.git
</pre>


- copy the demo's directory (iot-truck-streaming/) to the local filesystem under /root

- make the scripts executable:
- 
<pre>  
  cd iot-truck-streaming/
  chmod 750 *.sh setup/bin/*.sh
</pre>

- update config.properties with host names where your services run,  including the names of the supervisor nodes
	- NOTE: the demo will pick up the version of config.properties in etc/storm_demo at runtime

- update variables defined at the top in user-env.sh
	-user is ambari user (admin)
	-pass is ambari password (admin)
	-cluster is the name of cluster you will install demo on
	-host is the ambari url, eg: hdpdemo.hortonworks.comt:8080

- Execute the script installdemo.sh
	<pre>
		./installdemo.sh
	</pre>	
	(If the script is stuck trying to Stop Falcon. You would need to stop Falcon from Ambari.)
	
If you get error building this
<pre>
 cd 
 git clone https://github.com/DhruvKumar/hadoop-mini-clusters
 cd hadoop-mini-cluster
	mvn clean install -DskipTests

cd ../iot-truck-streaming

 rerun
 	./installdemo.sh

</pre>


- source root's bashrc ". /root/.bashrc"

- If on sandbox, run 'rundemo.sh clean', else run 'rundemo.sh'

- When you see the 
	"
	[INFO] Started Jetty Server" message, the demo is up at: 
	http://sandbox.hortonworks.com:8081/storm-demo-web-app/index.html
	
	"


In a subsequent run, you may want to do 'rundemo.sh clean' 
	- which will kill the topology, stop storm, cleanup storm dirs, and restart storm.

