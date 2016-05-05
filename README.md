This repo will holds a basic solr config, schema and xslt to use as a starting point for future projects.

It is now dependent on the [discoverygarden GSearch extensions](https://github.com/discoverygarden/dgi_gsearch_extensions)--which includes the Joda time library.

If one wishes to index Drupal content and users, one might process the `conf/data-import-config.xml.erb` into `conf/data-import-config.xml`. It takes three parameters:
* `drupal_dbname`
* `drupal_db_username`
* `drupal_db_password`

The 4.x branch is setup to utilize solr 4ish configurations. These have been successfully tested with solr 4.2.0. 

#### Localizations for UTK Digital Initiatives
* Changes for our development|production environment
	* paths have been changed from `/usr/local` to `/vhosts/fedora/`.
* Changes for testing in the Vagrant VM
	* paths have been retained.
* Modifications to islandora_transforms/slurp_all_MODS to reflect the nifty stuff happening in our MODS records.

#### Updating a file on the VM
* __Note:__ in order to view the latest changes, rsync the islandora_transforms/slurp_all_MODS_to_solr.xslt to vagrant@localhost:/var/lib/tomcat7/webapps/fedoragsearch/WEB-INF/classes/fgsconfigFinal/index/FgsIndex/islandora_transforms.
	* Don't forget to `$ sudo chown tomcat7:tomcat7` on the rsync'd file.
	* Restart Tomcat with the following:
		* `$ sudo su`
		* `# service tomcat7 restart`
	* Update a PID or add a new item to your repository and then check Solr (or however you want to view your Solr fields).
		* There are a couple of ways to do this:
			1) use the localhost:8080/fedoragsearch/rest interface > select the __updateIndex__ link > enter an appropriate PID in the _updateIndex fromPid_ text box and then click _updateIndex fromPid_.
			2) upload one of the test zips (available in JIRA).
		* Querying the Solr interface is a quick way to check on the new fields; e.g. `http://localhost:8080/solr/collection1/select?q=*%3A*&fq=PID%3Aislandora*&sort=PID+asc&fl=PID%2Cutk_mods_*&wt=xml&indent=true`

#### Note(s):
* Ensure that you're deploying the appropriate 4.x branch!
	* 4.x-vagrant for testing on your local VM.
	* 4.x for dev and prod.
* Ensure that you're using rsync to move files around - there are files in the target directories that need to stay there!
* conf/ belongs under /vhosts/fedora/solr/collection1.
* islandora_transforms/, foxmlToSolr, and index.properties belong under $CATALINA_HOME/webapps/fedoragsearch/WEB-INF/classes/fgsconfigFinal/index/FgsIndex/.