# ePuSta-Server

The ePuSta-Server provide AccessStatistics. Required is Logfile in epusta logformat. The statistics curently only accessable by an OAS compatible API. More APIs and a Webinterface comming soon. 

## Getting Started

### Prerequisites
* Linux 
* Solr 7

### Installation

* Clone the git-hub ePuSta-Server to a local directory via *git clone https://github.com/gbv/ePuSta-Server.git*
* Create a Core in Solr and copy the Files, located in the *solr* directory, in the *conf* directory of the core.
* Copy the file *config/config.template* to *config/config*
Edit the files deleteSolrCore.sh import.sh to set the SolrURL and core name.

To use the OAS compatible API see.

## Work with the Core

Scripts to work with the core are located in the directory *bin*.

### Import Data

The script createSolrImport.php transform the Logfiles, generated by the ePuSta-logfilepaser, to a solr importable json-file. There are two levels of generating:
* DEBUG - all loglines where transformed
* PROD - transform only loglines with an publication identifier 

Example: Create the import file reposas-2019-12-01.json from the file reposas.2019-12-01.log.
```
./createSolrImport.php --file=reposas.2019-12-01.log --level=PROD > reposas.2019-12-01.json
```

Push the data to the solr core.
```
/opt/solr/bin/post -c $SOLRCORE reposas.json
```
