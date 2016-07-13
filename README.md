## 4.x-vagrant branch ##

### About ###
This branch is configured for UTK Digital Initiatives' islandora_vagrant VMs. The repository holds a basic Solr config, a basic Solr schema, as well as the XSLT that Fedora Generic Search (fedoragsearch) uses to create Solr indexes.

The 4.x* branches are intended to be used with Solr 4.2.0.

#### Localizations for UTK DI ####
* Modifications to islandora_transforms/slurp_all_MODS to reflect the nifty stuff happening in our MODS records.

#### Deployment/Installation ####
* [solr-conf/\*](./solr-conf/) ---> `/usr/local/solr/collection1/conf/`
* [islandora_transforms](./islandora_transforms/) ---> `/var/lib/tomcat7/webapps/fedoragsearch/WEB-INF/classes/fgsconfigFinal/index/FgsIndex/`
* [foxmlToSolr.xslt](./foxmlToSolr.xslt) ---> `/var/lib/tomcat7/webapps/fedoragsearch/WEB-INF/classes/fgsconfigFinal/index/FgsIndex/`
* [index.properties](./index.properties) ---> `/var/lib/tomcat7/webapps/fedoragsearch/WEB-INF/classes/fgsconfigFinal/index/FgsIndex/`

#### Testing A Change to slurp_all_MODS ####
* Sync your changes using the utility/methodology of your choice.
* On your islandora_vagrant VM, `$ sudo chown tomcat7:tomcat7` on the updated slurp_all_MODS_to_solr.xslt.
* On your islandora_vagrant VM, restart Tomcat with the following: `$ sudo service tomcat7 restart`
* Update a PID or add a new item to your repository and then update your Solr index.
    * There are a variety of ways to do this; here are two:
        1) use the localhost:8080/fedoragsearch/rest interface > select the **updateIndex** link > enter an appropriate PID in the _updateIndex fromPid_ text box and then click _updateIndex fromPid_.
        2) ssh into your vagrant VM > run the following `curl` command using the PID of the updated item: `curl -u fedoraAdmin:fedoraAdmin -X GET "http://localhost:8080/fedoragsearch/rest?operation=updateIndex&action=fromPid&value=$YOUR_PID"`
* Query the Solr index from your browser: `http://localhost:8080/solr/collection1/select?q=%22$YOUR_PID_HERE%22&fl=PID%2Cutk_mods_*&df=PID&wt=xml&indent=true`. **Note:** depending on your browser you may need to escape the `:` in your PID; e.g. `islandora:3` vs `islandora%3A3`.

### Dependencies ###
It is now dependent on the [discoverygarden GSearch extensions](https://github.com/discoverygarden/dgi_gsearch_extensions)--which includes the Joda time library. **Note:** this dependency is included in the islandora_vagrant VM, under `/var/lib/tomcat7/webapps/fedoragsearch/WEB-INF/lib/`.

### Miscellany ###
If one wishes to index Drupal content and users, one might process the `conf/data-import-config.xml.erb` into `conf/data-import-config.xml`. It takes three parameters:

* `drupal_dbname`
* `drupal_db_username`
* `drupal_db_password`
