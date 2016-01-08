This repo will holds a basic solr config, schema and xslt to use as a starting point for future projects.

It is now dependent on the [discoverygarden GSearch extensions](https://github.com/discoverygarden/dgi_gsearch_extensions)--which includes the Joda time library.

If one wishes to index Drupal content and users, one might process the `conf/data-import-config.xml.erb` into `conf/data-import-config.xml`. It takes three parameters:
* `drupal_dbname`
* `drupal_db_username`
* `drupal_db_password`


[![Join the chat at https://gitter.im/utkdigitalinitiatives/basic-solr-config](https://badges.gitter.im/utkdigitalinitiatives/basic-solr-config.svg)](https://gitter.im/utkdigitalinitiatives/basic-solr-config?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)