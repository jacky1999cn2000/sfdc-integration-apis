# RESTful

* Several major differences between RESTful and SOAP
  * JSON vs XML
  * RESTful has concept of resource, so the URL now has meaning
  * HTTP Verbs now have meaning for RESTful APIs (they have no meanings for SOAP APIs)

* Created a connected app in sfdc

![1](./imgs/1.png)

* Login (Oauth type:password)

![2](./imgs/2.png)

* General Usage (GET method, with `Authorization:Bearer [token]` header)
`https://na40.salesforce.com/services/data/v35.0/sobjects/account`
`https://na40.salesforce.com/services/data/v35.0/sobjects/account/describe`
`https://na40.salesforce.com/services/data/v35.0/sobjects/voter__c`
`https://na40.salesforce.com/services/data/v35.0/sobjects/voter__c/a0146000000u4DBAAY`
`https://na40.salesforce.com/services/data/v35.0/sobjects/voter__c/describe`
`https://na40.salesforce.com/services/data/v35.0/query?q=select+name+from+Voter__c+where+Precinct__r.Name+='3rd District'`

* [Conditional Requests](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/intro_rest_conditional_requests.htm)

* Maximize Round Trips with Composite Calls (**see ppt for more detailed explanations**)
  * Batch up a set of operations
  * Created nested records
  * Create set of unrelated records

* Batch query (**note the url**)
  * request
  ```
  POST /services/data/v35.0/composite/batch HTTP/1.1
  Host: na40.salesforce.com
  Authorization: Bearer 00D46000000YxRg!ARIAQMiMeMTkzNKwgVjnmTOioxt87fcfHMmvMac0Xd9sL7K8hb3VmH55dvoqxJy8oxZvgQmwnUs_FLMcdPY.StevyCm9_Zu3
  Content-Type: application/json
  Cache-Control: no-cache
  Postman-Token: ed3ac57c-676a-5552-524a-05f69dfbe8a2

  {
  "batchRequests" : [
      {
      "method" : "GET",
      "url" : "v35.0/sobjects/Voter__c/a0146000000u4DBAAY"
      },{
      "method" : "GET",
      "url" : "v35.0/sobjects/Precinct__c/a0046000001SQszAAG"
      },{
      "method" : "GET",
      "url" : "v35.0/sobjects/Voter_Donation__c/a0246000001PsKSAA0?fields=Name,Candidate_Name__c"
      }]
  }
  ```

  * response
  ```
  {
    "hasErrors": false,
    "results": [
      {
        "statusCode": 200,
        "result": {
          "attributes": {
            "type": "Voter__c",
            "url": "/services/data/v35.0/sobjects/Voter__c/a0146000000u4DBAAY"
          },
          "Id": "a0146000000u4DBAAY",
          "IsDeleted": false,
          "Name": "Leslie Knope",
          "CreatedDate": "2017-02-27T22:24:33.000+0000",
          "CreatedById": "00546000000piQWAAY",
          "LastModifiedDate": "2017-02-27T22:24:33.000+0000",
          "LastModifiedById": "00546000000piQWAAY",
          "SystemModstamp": "2017-02-27T22:24:33.000+0000",
          "LastViewedDate": "2017-02-28T02:06:35.000+0000",
          "LastReferencedDate": "2017-02-28T02:06:35.000+0000",
          "Contacted_2016__c": false,
          "Last_Contact_Date__c": null,
          "Mailing_Address__c": "3738 247th Ave SE, Issaquah, WA 98029",
          "Political_Party__c": "Democrat",
          "Precinct__c": "a0046000001SQszAAG"
        }
      },
      {
        "statusCode": 200,
        "result": {
          "attributes": {
            "type": "Precinct__c",
            "url": "/services/data/v35.0/sobjects/Precinct__c/a0046000001SQszAAG"
          },
          "Id": "a0046000001SQszAAG",
          "OwnerId": "00546000000piQWAAY",
          "IsDeleted": false,
          "Name": "3rd District",
          "CreatedDate": "2017-02-27T22:23:25.000+0000",
          "CreatedById": "00546000000piQWAAY",
          "LastModifiedDate": "2017-02-27T22:23:25.000+0000",
          "LastModifiedById": "00546000000piQWAAY",
          "SystemModstamp": "2017-02-27T22:23:25.000+0000",
          "LastViewedDate": "2017-02-28T02:46:32.000+0000",
          "LastReferencedDate": "2017-02-28T02:46:32.000+0000"
        }
      },
      {
        "statusCode": 200,
        "result": {
          "attributes": {
            "type": "Voter_Donation__c",
            "url": "/services/data/v35.0/sobjects/Voter_Donation__c/a0246000001PsKSAA0"
          },
          "Name": "DN-00000",
          "Candidate_Name__c": "Garry Gergich",
          "Id": "a0246000001PsKSAA0"
        }
      }
    ]
  }
  ```

* Batch Create (**note the url**)
  * request
  ```
  POST /services/data/v35.0/composite/tree/Precinct__c HTTP/1.1
  Host: na40.salesforce.com
  Authorization: Bearer 00D46000000YxRg!ARIAQMiMeMTkzNKwgVjnmTOioxt87fcfHMmvMac0Xd9sL7K8hb3VmH55dvoqxJy8oxZvgQmwnUs_FLMcdPY.StevyCm9_Zu3
  Content-Type: application/json
  Cache-Control: no-cache
  Postman-Token: 945456a8-d423-58c7-652c-477b1fa5ca7d

  {

    "records": [
    	{

  	"attributes": {"type": "Precinct__c", "referenceId": "ref1"},

  	"Name": "4th District"

  	},

  	{

  	"attributes": {"type": "Precinct__c", "referenceId": "ref2"},

  	"Name": "5th District"

  	}

      ]

  }
  ```

  * response
  ```
  {
    "hasErrors": false,
    "results": [
      {
        "referenceId": "ref1",
        "id": "a0046000001SRcxAAG"
      },
      {
        "referenceId": "ref2",
        "id": "a0046000001SRcyAAG"
      }
    ]
  }
  ```

* Batch Create with nested relationships (**note the url**)
  * request
  ```
  POST /services/data/v35.0/composite/tree/Voter__c HTTP/1.1
  Host: na40.salesforce.com
  Authorization: Bearer 00D46000000YxRg!ARIAQMiMeMTkzNKwgVjnmTOioxt87fcfHMmvMac0Xd9sL7K8hb3VmH55dvoqxJy8oxZvgQmwnUs_FLMcdPY.StevyCm9_Zu3
  Content-Type: application/json
  Cache-Control: no-cache
  Postman-Token: 916d1045-11fe-b64d-1dee-ef40cd2c2e82

  {

  	"records": [{

  		"attributes": {"type": "Voter__c", "referenceId": "ref1"},

  		"Name": "Ann Perkins",

  		"Precinct__c": "a0046000001SQszAAG",

  		"Mailing_Address__c": "3726 257th Ave SE, Issaquah, WA 98029",
  		"Political_Party__c": "Independent",
  		"Voter_Donations__r": {

  			"records": [{

  				"attributes": {"type": "Voter_Donation__c", "referenceId": "ref2"},

  				"Amount__c": 1000,
  				"Candidate_Name__c": "Mike Smith"
  			},
  			{

  				"attributes": {"type": "Voter_Donation__c", "referenceId": "ref3"},

  				"Amount__c": 500,
  				"Candidate_Name__c": "Tim Westwood"
  			},
  			{

  				"attributes": {"type": "Voter_Donation__c", "referenceId": "ref4"},

  				"Amount__c": 100,
  				"Candidate_Name__c": "Tom Haverford"
  			}]

  		}

  	}]

  }
  ```

  * response
  ```
  {
    "hasErrors": false,
    "results": [
      {
        "referenceId": "ref1",
        "id": "a0146000000u58HAAQ"
      },
      {
        "referenceId": "ref2",
        "id": "a0246000001PtSGAA0"
      },
      {
        "referenceId": "ref3",
        "id": "a0246000001PtSHAA0"
      },
      {
        "referenceId": "ref4",
        "id": "a0246000001PtSIAA0"
      }
    ]
  }
  ```

  * Custom REST Service via Apex (ommited)
