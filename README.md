## 4.x branch ##

### About ###
This branch is configured for UTK Digital Initiatives' development and production servers. The repository holds Fedora configuration files, Fedora Generic Search (fedoragsearch) configuration files, Solr config files and schema, as well as the XSLT that fedoragsearch uses to create Solr indexes.

The 4.x* branches are intended to be used with Solr 4.2.0.

#### Localization for UTK DI ####
* Multi-threading updates to [Fedora](fedora-conf) and [fedoragsearch](fedoragsearch-conf). See [Discovery Garden's wiki](https://github.com/discoverygarden/basic-solr-config/wiki/performance-tuning-for-multithreaded-solr-ingest) for more information.
* Configuration changes to [Solr](solr-conf).
* Modifications to [islandora_transforms](islandora_transforms)
    * (directory|file) paths have been updated to reflect local (directory|file) paths.
    * changes to slurp_all_MODS_to_solr.xslt to reflect the nifty stuff happening in our MODS records.
* (Directory|File) paths have been modified to reflect local deployment paths.

#### Deployment/Installation ####
* [fedora-conf/fedora.fcfg](./fedora-conf/fedora.fcfg) ---> `/vhosts/fedora/server/config/`
* [fedoragsearch-conf/fedoragsearch.properties](./fedoragsearch-conf/fedoragsearch.properties) ---> `/vhosts/fedora/tomcat/webapps/fedoragsearch/WEB-INF/classes/fgsconfigFinal/`
* [fedoragsearch-conf/updater](./fedoragsearch-conf/updater) ---> `/vhosts/fedora/tomcat/webapps/fedoragsearch/WEB-INF/classes/fgsconfigFinal/` **note:** replaces the entire directory
* [islandora_transforms](islandora_transforms) ---> `/vhosts/fedora/tomcat/webapps/fedoragsearch/WEB-INF/classes/fgsconfigFinal/index/FgsIndex/`
* [foxmlToSolr.xslt](foxmlToSolr.xslt) ---> `/vhosts/fedora/tomcat/webapps/fedoragsearch/WEB-INF/classes/fgsconfigFinal/index/FgsIndex/`
* [index.properties](index.properties) ---> `/vhosts/fedora/tomcat/webapps/fedoragsearch/WEB-INF/classes/fgsconfigFinal/index/FgsIndex/`
* [solr-conf/\*](solr-conf/) ---> `/vhosts/fedora/solr/collection1/conf/`

**Note:** Re-deployments should be done in conjunction with a Tomcat restart to ensure that all classes are loaded correctly.

### Dependencies ###
It is now dependent on the [discoverygarden GSearch extensions](https://github.com/discoverygarden/dgi_gsearch_extensions)--which includes the Joda time library.

### Miscellany ###
If one wishes to index Drupal content and users, one might process the `conf/data-import-config.xml.erb` into `conf/data-import-config.xml`. It takes three parameters:

* `drupal_dbname`
* `drupal_db_username`
* `drupal_db_password`