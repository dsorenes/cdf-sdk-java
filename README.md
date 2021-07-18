[![java-main Actions Status](https://github.com/cognitedata/cdf-sdk-java/workflows/java-main/badge.svg)](https://github.com/cognitedata/cdf-sdk-java/actions)

<a href="https://cognite.com/">
    <img src="https://raw.githubusercontent.com/cognitedata/cognite-python-docs/master/img/cognite_logo.png" alt="Cognite logo" title="Cognite" align="right" height="80" />
</a>

# Java sdk for CDF

The Java SDK provides convenient access to Cognite Data Fusion's capabilities. It covers a large part of CDF's
capability surface, including experimental features. In addition, it is designed to handle a lot of the client "chores"
for you so you can spend more time on your core client logic.

Some of the SDK's capabilities:
- _Upsert support_. It will automatically handle `create`and `update` for you.
- _Retries with backoff_. Transient failures will automatically be retried.
- _Performance optimization_. The SDK will handle batching and parallelization of requests.

Please refer to [the documentation](https://github.com/cognitedata/cdf-sdk-java/blob/main/docs/index.md) for more
information ([https://github.com/cognitedata/cdf-sdk-java/blob/main/docs/index.md](https://github.com/cognitedata/cdf-sdk-java/blob/main/docs/index.md)).
    
### Installing the sdk

```xml
<dependency>    
    <groupId>com.cognite</groupId>
    <artifactId>cdf-sdk-java</artifactId>
    <version>0.9.6</version>
</dependency>
```
    
### Features
#### Core resource types
- Time series
- Assets
- Events
- Files
- Sequences
- Relationships
- Raw

#### Data organization
- Data sets
- Labels

#### Contextualization
- Entity matching
- Interactive P&ID (experimental)

## Quickstart
```java
// Create the Cognite client using API key as the authentication method
CogniteClient client = CogniteClient.ofKey(<yourApiKey>)
        .withBaseUrl("https://yourBaseURL.cognitedata.com");  //optional parameter
        
// ... or use client credentials (OpenID Connect)
CogniteClient client = CogniteClient.ofClientCredentials(
        <clientId>,
        <clientSecret>,
        TokenUrl.generateAzureAdURL(<azureAdTenantId>))
        .withBaseUrl("https://yourBaseURL.cognitedata.com"); //optional parameter     
        
// List all assets
List<Asset> listAssetsResults = new ArrayList<>();
client.assets()
        .list(Request.create()
                .withFilterParameter("key", "value"))       //optionally add filter parameters
        .forEachRemaining(assetBatch -> listAssetsResults.addAll(assetBatch));        //results are read in batches

// List all events
List<Events> listEventsResults = new ArrayList<>();
client.events()
        .list(Request.create()
                .withFilterParameter("key", "value"))       //optionally add filter parameters
        .forEachRemaining(eventBatch -> listEventsResults.addAll(eventBatch));        //results are read in batches

```


[![Open in Cloud Shell](http://gstatic.com/cloudssh/images/open-btn.svg)](https://console.cloud.google.com/cloudshell/editor?cloudshell_git_repo=https://github.com/cognitedata/cdf-sdk-java.git)
