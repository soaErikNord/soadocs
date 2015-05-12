#Akana Automated Software Deployment

##Installer Script
To run installer
* Download and copy the appropriate files to server (/tmp/install)
* cd <extracted location>/install
* Extract pso-automation.<version>_<date>.zip somewhere (unzip pso-automation.<version>_<date>.zip)
* chmod +x installer.py
* vi(or favorite editor) properties/installer.properties
* Update as needed
** resources
** key (license)
* add appropriate environment and container property files to properties directory
* run ./installer.py -i -s -c -v > createContainers.log
** -i install
** -s deploy scripts
** -c create containers
** -v verbose

###Main

###Install Base

###Install Scripts

##Container Script
To run container as standalone
* cd <install dir>/sm70/scripts/properties
* Update all property files correctly.  Delete the ones you don't want to create
* cd ..
* export JAVA_HOME=<install dir>/sm70/jre
* export JYTHON_HOME=<install dir>/sm70/scripts
* run ../bin/jython.sh containerManager.py -c -v > createContainers.log
** -c create containers
** -u update containers
** -v verbose

###Create Container

####Container Features
Install the proper features
* Standalone PM
** -policy.manager.console
** -policy.manager.services
** -security.services

* PM with CM
** -Install Standalone PM
** -community.manager
** -community.manager.default.theme
** -community.manager.openid.provider
** -community.manager.scheduled.jobs
** -community.manager.simple.developer.theme (If using SimpleDev)

* PM with CM and OAuth
** -Install PM with CM
** -community.manager.oauth.provider
** -oauth.provider

* PM with remote CM
** -Install Standalone PM
** -community.manager.scheduled.jobs
** -community.manager.plugin
** -community.manager.policy.console

* Standalone CM
** -community.manager.apis
** -community.manager.default.theme
** -community.manager.openid.provider
** -community.manager.simple.developer.theme (If using SimpleDev)

* Standalone CM with OAuth
** -Install Standalone CM
** -community.manager.oauth.provider
** -oauth.provider

* Standalone ND
** -network.director
** -api.security.policy.handler

* Standalone ND with OAuth
** -Install Standalone ND
** -community.manager.oauth.provider.agent
** -oauth.provider.agent

* Standalone OAuth
** -community.manager.oauth.provider
** -oauth.provider
** -community.manager.plugin

* Ping Support
** -For CM
*** -ping.federate.integration
** -For ND
*** -ping.support

* LaaS Support
** -For CM nodes only
*** -community.manager.laas
	
* Add Monitoring to any container
** -admin.monitoring.tool

###Update Features
		
##Property Files

###Installer Property File

 [InstallSection]
; install.path and resources.location must be absolute
install.path=/opt/soa_sw/
resources.location=/tmp/resources/
install.executable=Linux-pm-7.2.388-setup64.bin
features=<Update with all desired add on features>
; This sets the IATEMPDIR
temp.directory=/tmp
; Populate with the license key
key=
; For windows installs, this creates the short cut
shortcut=

###Environment Property File
A single environment property file is required for a given server build out.  These are properties that will be shared across all containers that exist on a given server.  Currently, support building database properties for MySQL and MSSQL.

[InstallSection]
install.path=/opt/soa_sw/

[DatabaseSection]
database.create=true
database.pm=true
database.cm=false
database.oauth=false
;  	Specify the configuration values for this database
;    	key       |restrict | description         
;   -------------+---------+--------------------------------------------------
;   databaseType |         | 'mssql', 'mysql', 'oracle', 'oracle-sn', 'db2'
;   user         |         | Database connect userid
;   password     |         | Plain-text password for that user
;   server       |         | Database host name
;   port         |         | Database port
;   database     |         | Name of the database (tablespace for oracle*)
;   instance     | mssql   | MS SQL Server "instance name"
;   instanceName | oracle* | Oracle SID or Service Name (for oracle-sn)
;   tablespace   | db2     | DB/2 Table Space name
;   bufferName   | db2     | DB/2 Buffer Pool
;   isNewBuffer  | db2     | flag to create a new Buffer Pool
;   maxPoolSize  |         | Maximum number of database connections
;   minPoolSize  |         | Minimum number of open, idle connections
;   maxWait      |         | Maximum time to wait for an available connection
;   -------------+---------+--------------------------------------------------
; Common Properties
database.type=
database.user=
database.password=
database.admin=
database.admin.password=
database.host=
database.port=
; For oracle use the tablespace
database.name=
database.max.pool.size=30
database.min.pool.size=3
database.max.wait=30000
database.jar=
; mssql/oracle specific, only populate for mssql or oracle
database.instance.name=
; db2 specific, only populate for db2
database.tablespace=
database.bufferName=
database.isNewBuffer=

[ProxySection]
proxy.url=
proxy=
proxy.user=
proxy.password=

###Container Property Files
A uniquely named container file should be provided for every container that needs to be built and configured for a specific environment.  So, if a PM and ND nodes are needed an a single host, it would be required for 2 uniquely named container property files.

For a secured container, include the secured flag as true.  If custom certificates are needed, provide 2 different custom keystores.  The first keystore would be used for the container that is being built.  The trusted keystore will be used to add a certificate to the cacert file for any containers that this container needs to interact with.  At the same time, the 'com.soa.security' category will be appropriately updated and the crl flag will be set to false in the 'com.soa.crl' category.

 [CommonProperties]
container.name=pm
container.host=0.0.0.0
container.port=9900
container.admin.port=8900
container.admin.user=administrator
container.admin.password=password
container.secure=false
container.secure.keystore=
container.secure.storepass=
container.secure.alias=
container.secure.trusted.keystore=
container.secure.trusted.storepass=
container.secure.trusted.alias=

[FeaturesSection]
agent.foundation=false
community.manager=false
community.manager.apis=false
community.manager.default.theme=false
community.manager.oauth.provider=false
community.manager.oauth.provider.agent=false
community.manager.openid.provider=false
community.manager.scheduled.jobs=false
community.manager.simple.developer.theme=false
delegate=false
delegate.access.point=false
development.services.feature=false
managed.services=false
network.director=false
oauth.provider=false
oauth.provider.agent=false
ping.support=false
policy.manager.console=true
policy.manager.services=true
scheduled.jobs=false
security.services=false
tomcat.agent=false

[PluginSection]
api.security.policy.handler=false
cluster.support=false
community.manager.plugin=true
community.manager.policy.console=true
external.keystore.feature=false
kerberos.implementation=false
community.manager.laas=false
ping.federate.integration=false

[ToolSection]
72.upgrade=false
admin.monitoring.tool=true

[ConfigurationFiles]
database.configure=true
proxy.filename=
; used to route containers through load balancer when needed
; Format needs to be the following '<routes><route><filename>com.soa.http.route-pm1.cfg</filename><pattern>http://pm.host.com:9900/*</pattern><url>http://lb.host.com</url></route></routes>'
; Needed when routing requests back through a load balance: https://support.soa.com/support/index.php?_m=knowledgebase&_a=viewarticle&kbarticleid=607
route.definitions=<routes><route><filename>com.soa.http.route-pm1.cfg</filename><pattern>http://pm.host.com:9900/*</pattern><url>http://lb.host.com</url></route></routes>

; ND specific properties
; just the address to pm like http://<hostname>:<port>
wsmex.address=
; org needs to be a valid uddi key (Change if container needs to be in a different organization)
; Change if ND is required to be under a different organization
org=uddi:soa.com:registryorganization
cluster=
https.private.key=
https.private.key.cert.chain=
https.trusted.cert.chain=

[TenantProperties]
; CM specific properties
atmosphere.context.root=
tenant.url=http://localhost:9900 
tenant.name=EnterpriseAPI 
tenant.id=enterpriseapi
tenant.address=http://localhost:9900 
tenant.console.address=http://localhost:9900/enterpriseapi 
tenant.theme=default 
tenant.admin.email=administrator@localhost.localdomain 
tenant.admin.password=password 
tenant.contact.email.address=no-reply@localhost.localdomain 
tenant.from.email.address=no-reply@localhost.localdomain
tenant.virtual.hosts=

[HardeningProperties]
; Hardening properties are set to recommended values.  Change if desired.  For details review: http://docs.akana.com/sp/platform-hardening.html
container.harden=true
harden.ignoreCookies=ignoreCookies
harden.secureCookies=true
harden.cipherSuites=SSL_RSA_WITH_RC4_128_MD5,SSL_RSA_WITH_RC4_128_SHA,TLS_RSA_WITH_AES_128_CBC_SHA,TLS_DHE_DSS_WITH_AES_128_CBC_SHA,SSL_RSA_WITH_3DES_EDE_CBC_SHA,SSL_DHE_DSS_WITH_3DES_EDE_CBC_SHA
harden.cache.expirationPeriod=3600000
harden.cache.refreshTime=300000
; only configured on ND containers
harden.nd.interceptor.blocked=content-type,content-length,content-range,content-md5,host,expect,keep-alive,connection,transfer-encoding,atmo-forward-to,atmo-forwarded-from
; only configured on CM Containers
harden.cm.interceptor.blocked=content-type,content-length,content-range,content-md5,host,expect,keep-alive,connection,transfer-encoding

[PerformanceProperties]
; Performance properties need to be set appropriately for your desired results.  Values currently set are for examples only.
;    For details review: http://docs.akana.com/sp/performance-tuning.html
container.performance=true
performance.connection.maxTotal=2000
performance.connection.defaultMaxPerRoute=1500
performance.loadGifMetrics=false
performance.performAutoSearch=true
performance.requireMetricsPolicy=true
; ND containers to controll the usage writer
performance.queueCapacity=10000
performance.usageBatchSize=50
performance.writeInterval=1000
performance.preloadInvokedServices=true
performance.framework.idleExpiration=259200
performance.framework.makeFreshInterval=900
performance.endpoint.allowRemoval=false
performance.endpoint.expirationInterval=3600000
performance.endpoint.maxrefreshInterval=900000



