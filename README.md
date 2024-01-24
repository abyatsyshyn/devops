# IDUN Neo4j Graph DB Server Service & Operations

# Description

<span style="font-size: large;">This document is intended to acquaint those who may be concerned with how to deploy, operate and maintain the Idun Neo4j Graph Database Server. All of the following applies to the</span><span style="font-size: large;"><span lang="en-US"> Idun </span></span><span style="font-size: large;">Production</span><span style="font-size: large;"><span lang="en-US"> Neo4j </span></span><span style="font-size: large;">Server as of January 25, 2022.</span>

# Deployment.

<a name="8111b592-d049-462e-8cd2-6f9cf000038e"></a><a name="72bacf8a-1471-4f5f-9083-89aee9d0c074"></a> <span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;">The</span></span></span> <span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="en-US">***Enterprise Neo4j Server v.***</span></span></span></span><span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="en-US">***4.3.6***</span></span></span></span> <span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"> is deployed in a separate resource group </span></span></span><span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;">***idun-neo4j-43-rg***</span></span></span><span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;">, using a pre-installed Azure Marketplace image. The server is running on </span></span></span><span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;">***Standard D16as v4 (16 vcpus, 64 GiB memory)*** </span></span></span><span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="en-US">Azure</span></span></span></span> <span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="en-US">virtual machine type and called </span></span></span></span><span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="en-US">***idun-neo4j-vm (ip: 51.124.153.198)***</span></span></span></span><span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="en-US"> :</span></span></span></span>

[![image-1644390623781.png](http://bookstackapp.proptechos.com:8080/uploads/images/gallery/2022-02/scaled-1680-/image-1644390623781.png)](http://bookstackapp.proptechos.com:8080/uploads/images/gallery/2022-02/image-1644390623781.png)

<span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="en-US">Graph is available on the: </span></span></span></span><span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="en-US">*prod.neo4j.proptechos.com*</span></span></span></span>

# User management and access.

<span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"> When first starting a Neo4j DBMS, there is always a single default user </span></span></span>`<span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><em>neo4j </em></span></span></span>`<span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;">with administrative privileges. It is possible to set the initial password using </span></span></span><span style="color: #000080;"><span lang="zxx">[<span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;">*neo4j-admin set-initial-password*</span></span></span>](https://neo4j.com/docs/operations-manual/4.4/configuration/set-initial-password/)</span></span><span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;">, otherwise it is necessary to change the password after the first login.</span></span></span> <span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="en-US">The password of the </span></span></span></span><span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="en-US">*neo4j*</span></span></span></span><span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="en-US"> user, like all our passwords and keys, it is saved in 1Password app in the Devops Vault.</span></span></span></span>

<span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="en-US"> All the rest user’s credentials of the corresponding</span></span></span></span> <span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="en-US">customer’s environments also stored in the corresponding records of the 1Password vault. </span></span></span></span>

# Security and restrictions.

<span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="en-US"> Ne</span></span></span></span><span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;">o4j</span></span></span><span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="en-US"> allow us to use </span></span></span></span><span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;">role-based access control and fine-grained security </span></span></span><span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="en-US">in it operations and usage.</span></span></span></span>

<span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;">Neo4j has a complex security model stored in the system graph, maintained in a special database called the </span></span></span><span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;">*system*</span></span></span><span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"> database. All administrative commands need to be executing against the </span></span></span><span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;">*system*</span></span></span><span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"> database. When connected to the DBMS over bolt, administrative commands are automatically routed to the system database.</span></span></span>

<span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"> Neo4j supports the securing of communication channels using standard SSL/TLS technology. </span></span></span><span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="en-US">On the server installed Lets Encrypt cert-bot, for new certificates obtaining and its maintenance. </span></span></span></span>

**<span style="color: #150e3d;"><span style="font-size: large;"><span lang="en-US">Install LetsEncrypt</span></span></span><span style="color: #150e3d;"><span style="font-size: large;"><span lang="uk-UA">.</span></span></span>**

<span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="uk-UA">Here is how we generate the certificate - </span></span></span></span><span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="uk-UA">*sudo certbot certonly*</span></span></span></span><span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="uk-UA">. As shown in the following, we’re specifying option 1 (we want to create a temporary webserver on port 80 to verify ourselves) and providing the domain name we’re generating a cert for (node.graph.c</span></span></span></span><span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="en-US">om</span></span></span></span><span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="uk-UA">)</span></span></span></span>

```
$ sudo certbot certonly
Saving debug log to /var/log/letsencrypt/letsencrypt.logHow would you like to authenticate with the ACME CA?
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
1: Spin up a temporary webserver (standalone)
2: Place files in webroot directory (webroot)
- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -
Select the appropriate number [1-2] then [enter] (press 'c' to cancel): 1
Plugins selected: Authenticator standalone, Installer None
Starting new HTTPS connection (1): acme-v02.api.letsencrypt.org
Please enter in your domain name(s) (comma and/or space separated)  (Enter 'c'to cancel):  node.graph.com
Obtaining a new certificate
Performing the following challenges:
http-01 challenge for node.graph.com 
Waiting for verification...
Cleaning up challengesIMPORTANT NOTES: 
- Congratulations! Your certificate and chain have been saved at:   /etc/letsencrypt/live/node.graph.com/fullchain.pem   Your key file has been saved at:   /etc/letsencrypt/live/node.graph.com/privkey.pem   
Your cert will expire on 2018-12-16. To obtain a new or tweaked   version of this certificate in the future, simply run certbot   again. To non-interactively renew *all* of your certificates, run   "certbot renew" 
- If you like Certbot, please consider supporting our work by:   Donating to ISRG / Let's Encrypt:   https://letsencrypt.org/donate   Donating to EFF: https://eff.org/donate-le
$
```

<span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="uk-UA">The success message at the bottom says we now have certificates located in the /etc/letsencrypt/live/\* subdirectories. </span></span></span></span>

**<span style="font-size: large;"><span lang="en-US">Neo4j SSL Framework configuration.</span></span>**

<span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="uk-UA">LetsEncrypt maintains these certificates in a directory called “live”. These are actually symlinks to files in another directory. This layer of indirection allows the certbot program to update the certificates periodically as needed, so that you don’t have to change cert locations.</span></span></span></span>

<span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="uk-UA">So when we place these into the neo4j structure, we’re going to be careful to create symlinks and not copy the files. By doing so, we can take advantage of the refresh abilities of Let’s Encrypt we might want later on.</span></span></span></span>

<span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="uk-UA">The first thing we have to do is adjust the very tight permissions on the certificates directory, by changing group ownership to neo4jand to make them readable by Neo4j.</span></span></span></span>

```
# Change group of all letsencrypt files to neo4j
sudo chgrp -R neo4j /etc/letsencrypt/* # Make sure all directories and files are group readable.
sudo chmod -R g+rx /etc/letsencrypt/* 
```

<span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="uk-UA">Next, we set up symlinks and the directory structure neo4j expects.</span></span></span></span>

<span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="uk-UA">Our version of Neo4j configuring with SSL per “connector” (bolt, HTTPS, cluster), means that each connector has its own directory with certificates. </span></span></span></span>

```
cd /var/lib/neo4j/certificates# Move old default stuff into a backup directory.
sudo mkdir bak
for certsource in bolt cluster https ; do
   sudo mv $certsource bak/
donesudo mkdir bolt
sudo mkdir cluster
sudo mkdir httpsexport MY_DOMAIN=graph.somehost.comfor certsource in bolt cluster https ; do
   sudo ln -s /etc/letsencrypt/live/$MY_DOMAIN/fullchain.pem $certsource/neo4j.cert
   sudo ln -s /etc/letsencrypt/live/$MY_DOMAIN/privkey.pem $certsource/neo4j.key
   sudo mkdir $certsource/trusted
   sudo ln -s /etc/letsencrypt/live/$MY_DOMAIN/fullchain.pem $certsource/trusted/neo4j.cert ;
done# Finally make sure everything is readable to the database
sudo chgrp -R neo4j *
sudo chmod -R g+rx *
```

<span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="uk-UA">Finally, we make adjustments to our neo4j configuration file. (Keeping in mind that if you’re using cloud VM images, this is </span></span></span></span>`<span style="color: #292929;"><span style="font-family: Menlo, Monaco, Courier New, Courier, monospace;"><span style="font-size: small;"><span lang="uk-UA">/etc/neo4j/neo4j.template</span></span></span></span>`<span style="color: #292929;"><span style="font-family: charter, Georgia, Cambria, Times New Roman, Times, serif;"><span style="font-size: medium;"><span lang="uk-UA">, </span></span></span></span><span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="uk-UA">and in other environments it’s </span></span></span></span>`<span style="color: #292929;"><span style="font-family: Menlo, Monaco, Courier New, Courier, monospace;"><span style="font-size: small;"><span lang="uk-UA">/etc/neo4j/neo4j.conf</span></span></span></span>`<span style="color: #292929;"><span style="font-family: charter, Georgia, Cambria, Times New Roman, Times, serif;"><span style="font-size: medium;"><span lang="uk-UA">)</span></span></span></span>

```
dbms.default_listen_address=0.0.0.0
dbms.default_advertised_address=your.hostname.com# BOLT Connector
dbms.connector.bolt.tls_level=REQUIRED
dbms.ssl.policy.bolt.enabled=true
dbms.ssl.policy.bolt.private_key=/var/lib/neo4j/certificates/bolt/neo4j.key
dbms.ssl.policy.bolt.public_certificate=/var/lib/neo4j/certificates/bolt/neo4j.cert
dbms.ssl.policy.bolt.client_auth=NONE# HTTPS connector
dbms.connector.https.enabled=true
dbms.ssl.policy.https.enabled=true
dbms.ssl.policy.https.client_auth=NONE
dbms.ssl.policy.https.private_key=/var/lib/neo4j/certificates/https/neo4j.key
dbms.ssl.policy.https.public_certificate=/var/lib/neo4j/certificates/https/neo4j.cert# Directories
dbms.ssl.policy.bolt.base_directory=/var/lib/neo4j/certificates/bolt
dbms.ssl.policy.https.base_directory=/var/lib/neo4j/certificates/https
```

<span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="en-US">It should be noticed that </span></span></span></span>*<span style="color: #292929;"><span style="font-family: charter, Georgia, Cambria, Times New Roman, Times, serif;"><span style="font-size: medium;">port 7474</span></span></span>* <span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="en-US">on our neo4j instance, which is responsible for </span></span></span></span>*<span style="color: #292929;"><span style="font-family: charter, Georgia, Cambria, Times New Roman, Times, serif;"><span style="font-size: medium;"><span lang="en-US">HTTP access</span></span></span></span><span style="color: #292929;"><span style="font-family: charter, Georgia, Cambria, Times New Roman, Times, serif;"><span style="font-size: medium;"><span lang="en-US">.</span></span></span></span>*

# Backups schedule and mechanism.

<span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="en-US">Backing up the database is performed on a schedule, every hour. The results are saved on </span></span></span></span><span style="color: #000080;"><span lang="zxx">[<span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="en-US">Azure Fileshare</span></span></span></span>](https://idundevopsrgdiag.file.core.windows.net/neobackups)</span></span><span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="en-US">.</span></span></span></span>

<span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="en-US">Backup creating script:</span></span></span></span>

```
#!/bin/bash

# creating Neo4J Graph DB daily backup

now=`date '+%d_%m_%Y_%H_%M_%S'`







export HEAP_SIZE=2G




sudo neo4j-admin backup --verbose --backup-dir=/home/idun/backups --database=system

sudo neo4j-admin backup --verbose --backup-dir=/home/idun/backups --database=neo4j

sudo neo4j-admin backup --verbose --backup-dir=/home/idun/backups --database=idun-vkprod-db

sudo neo4j-admin backup --verbose --backup-dir=/home/idun/backups --database=idun-yitprod-db

sudo neo4j-admin backup --verbose --backup-dir=/home/idun/backups --database=idun-multiprod01-db

sudo neo4j-admin backup --verbose --backup-dir=/home/idun/backups --database=idun-user-management-db




sudo tar -C /home/idun -czvf backups/neo4j_DB_$now.tar.gz backups/




sudo cp /home/idun/backups/neo4j_DB_$now.tar.gz /mnt/neobackups/neo4j_DB_$now.tar.gz

sudo rm -rf /home/idun/backups/*.*
```

<span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="en-US">Backup recovering script:</span></span></span></span>

> ```
> <span style="color: #150e3d;"><code class="language-">#!/bin/bash<br></br>service neo4j stop<br></br><br></br>neo4j-admin restore --from=/home/idun/backups/system --verbose --database=system --force<br></br>neo4j-admin restore --from=/home/idun/backups/neo4j --verbose --database=neo4j --force<br></br>neo4j-admin restore --from=/home/idun/backups/idun-vkprod-db --verbose --database=idun-vkprod-db --force<br></br>neo4j-admin restore --from=/home/idun/backups/idun-yitprod-db --verbose --database=idun-yitprod-db --force<br></br>neo4j-admin restore --from=/home/idun/backups/idun-multiprod01-db --verbose --database=idun-multiprod01-db --force<br></br>cd /var/lib/neo4j/data/databases/<br></br>chown -R neo4j:neo4j system/<br></br>chown -R neo4j:neo4j neo4j/<br></br>chown -R neo4j:neo4j idun-vkprod-db/<br></br>chown -R neo4j:neo4j idun-yitprod-db/<br></br>chown -R neo4j:neo4j idun-multiprod01-db/</code></span>
> ```
> 
> <span style="color: #150e3d;"><span style="font-family: Muli, serif;"><span style="font-size: large;"><span lang="en-US">Archives older than 7 days are removed from the repository every week.</span></span></span></span>
