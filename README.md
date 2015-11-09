## Introduction

This document describes what an archive should contain to be used with [(M|S)MSImporter](https://github.com/axelhenry/msmsimporter/)

### Archive format

.tar or .tar.gz. Your call.

### Archive content

Your archive should contain one file containing your smses (sms.json), and/or one file containing your mmses (mms.json).

![Content of an archive](https://github.com/axelhenry/msmsimporter-archive/raw/master/src/common/images/archive.png "Archive's content")

### sms.json

This file contains an array of [SMS](#sms). By specification, this document must be encoded in UTF-8.

#### SMS

A SMS is represented by 4 keys, all mandatory:
- __timestamp__
- __to__
- __body__
- __sent__
```javascript
{  
  "timestamp": 1319070778,  
  "to": "xxxxxxxxx",  
  "body": "You left something.",  
  "sent": false  
}
```

##### Data types

- __timestamp__ : integer
- __to__ : String
- __body__ : String
- __sent__ : boolean

### mms.json

This file contains an array of [MMS](#mms). By specification, this document must be encoded in UTF-8.

#### MMS

A MMS is represented by 8 keys:
- __timestamp__
- __to__
- __transactionid__
- __sent__
- subject
- pathToAttachment
- attachmentName
- mimeType

Only __timestamp__, __to__, __transactionid__ and __sent__ must have value. Others keys can be null or not included.   
However for a MMS to be valid, one of these conditions must be true:
- subject is defined
- pathToAttachment, attachmentName and mimeType are defined

WARNING : pathToAttachment is relative to your archive, be aware of that.

Examples:

- all keys defined:
```javascript
{  
  "pathToAttachment": "n133AxrLaCQABXkh4E/SP_A0476.jpg",  
  "mimeType": "image/jpeg",  
  "to": [  
      "xxxxxxxxx"  
  ],  
  "transactionid": "n133AxrLaCQABXkh4E",  
  "timestamp": 1333563101,  
  "attachmentName": "SP_A0476.jpg",  
  "subject": "Nice !!!",  
  "sent": false  
}
```
- subject only:
```javascript
{  
    "timestamp": 1431605782,  
    "transactionid": "BgePofozEeSOmVwmCv0ZTA",  
    "sent": false,  
    "subject": "Yo.",  
    "to": [  
        "+xxxxxxxxx"  
    ]  
}
```
- attachment only:
```javascript
{  
  "pathToAttachment": "n133AxrLaCQABXkh4E/SP_A0476.jpg",  
  "mimeType": "image/jpeg",  
  "to": [  
      "xxxxxxxxx"  
  ],  
  "transactionid": "n133AxrLaCQABXkh4E",  
  "timestamp": 1333563101,  
  "attachmentName": "SP_A0476.jpg",  
  "sent": false  
}
```

##### Data types
- __timestamp__ : integer
- __to__ : String array
- __transactionid__ : String
- __sent__ : boolean
- subject : String
- pathToAttachment : String
- attachmentName : String
- mimeType : String
