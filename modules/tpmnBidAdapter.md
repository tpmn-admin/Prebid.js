# Overview

```
Module Name:  TPMN Bid Adapter
Module Type:  Bidder Adapter
Maintainer: develop@tpmn.co.kr
```

# Description

Connects to TPMN exchange for bids.

NOTE:
- TPMN bid adapter only supports MediaType BANNER, VIDEO.
- Multi-currency is not supported.


# Bid Parameters

## Common (Banner, Video)
{: .table .table-bordered .table-striped }
|       Name     |    Scope    |                 Description                |    Example    |     Type     |
| -------------- | ----------- | ------------------------------------------ | ------------- | ------------ |
| `inventoryId` | required | Ad Inventory id TPMN | 123 | Number |
| `publisherId` | required | Publisher id provided by TPMN | "tpmn" | String |
| `battr` | optional | Block IAB Category Codes | ["IAB-1"] | Array-String |
| `bidFloor` | optional | Minimum price in USD. bidFloor applies to a specific unit. | 1.50 | Number |

# Banner Ad Unit Config
```
  var adUnits = [{
      // Banner adUnit
      code: 'banner-div',
	  mediaTypes: {
		  banner: {
		    sizes: [[300, 250], [320, 50]],  // banner size
        ... // battr
		  }
	  },
    bids: [
      {
        bidder: 'tpmn',
        params: {
          inventoryId: '1',       // required
          publisherId: 'TPMN',    // required
          bidFloor: 1.2,          // optional
          ... // bcat, badv, bapp // optional
        }
      }
    ]
    }];
```


# mediaTypes Parameters

## mediaTypes.banner

The following banner parameters are supported here so publishers may fully declare their banner inventory:

{: .table .table-bordered .table-striped }
|    Name   |    Scope    |                      Description                                  |  Example  |    Type   |
| --------- | ------------| ----------------------------------------------------------------- | --------- | --------- |
| sizes | required | Avalaible sizes supported for banner ad unit | [ [300, 250], [300, 600] ] | [[Integer, Integer], [Integer, Integer]] | 
## mediaTypes.video

We support the following OpenRTB params that can be specified in `mediaTypes.video` or in `bids[].params.video`

-  'mimes'
-  'minduration'
-  'maxduration'
-  'placement'
-  'protocols'
-  'startdelay'
-  'skip'
-  'skipafter'
-  'minbitrate'
-  'maxbitrate'
-  'delivery'
-  'playbackmethod'
-  'api'
-  'linearity'
-  'battr'


# Video Ad Unit Config
```
  var adUnits = [{
        code: 'video-div',
        mediaTypes: {
            video: {
                context: 'instream',                  // required
                mimes: ['video/mp4'],                 // required
                skippable: true,                      // optional
                minduration: 5,                       // optional
                maxduration: 30,                      // optional
                startdelay: 5,                        // optional
                playbackmethod: [1,3],                // optional
                api: [ 1, 2 ],                        // optional
                protocols: [ 2, 3 ],                  // optional
                linearity: 1,                         // optional
                placement: 2,                         // optional
                minbitrate: 10,                       // optional
                maxbitrate: 10                        // optional
                battr: [ 13, 14 ],                    // optional
            }
        },
        bids: [{
            bidder: 'tpmn',
            params: {
                inventoryId: '2',       // required
                publisherId: 'TPMN',    // required
                ... // bcat, badv, bapp
            }
        }]
    }];
```