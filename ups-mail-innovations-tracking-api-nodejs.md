UPS Mail Innovations Tracking API - Node.js
================================
Use Node.js to track UPS Mail Innovations shipments with UPS Mail Innovations Tracking API.

Features
--------
- Real-time UPS Mail Innovations tracking.
- Batch UPS Mail Innovations tracking.
- Other features to manage your UPS Mail Innovations tracking.

Installation
------------

Installation is easy:

    $ npm install trackingmore-sdk-nodejs

Quick Start
----------
Get the API key:

To use this API, you need to generate your API key.

- <a href="https://admin.trackingmore.com/developer/apikey" target="_blank" rel="noreferrer">
  Click here</a> to access TrackingMore admin.

- Go to the "Developer" section.

- Click "Generate API Key".

- Give a name to your API key, and click "Save" .


Then, start to track your UPS Mail Innovations shipments.

Usage
----------

Create a tracking (Real-time tracking):

      const TrackingMore = require('trackingmore-sdk-nodejs')
      const key = 'your api key'
      const trackingmore = new TrackingMore(key)
      
      const params = {
        'tracking_number': '92612903104062543400000915',
        'courier_code': 'ups-mi',
        'order_number': '',
        'customer_name': '',
        'title': '',
        'language': 'en',
        'note': 'test Order'
      }
      trackingmore.trackings.createTracking(params)
        .then(result => console.log(result))
        .catch(e => console.log(e))


Create trackings (Max. 40 tracking numbers create in one call):

    const TrackingMore = require('trackingmore-sdk-nodejs')
    const key = 'your api key'
    const trackingmore = new TrackingMore(key)
    
    const params = [{
        'tracking_number': '92419999920412543483090901',
        'courier_code':'ups-mi'
    },{
      'tracking_number': '92419999920594513018295593',
      'courier_code':'ups-mi'
    }]
    trackingmore.trackings.batchCreateTrackings(params)
      .then(result => console.log(result))
      .catch(e => console.log(e))



Get status of the shipment:

    const TrackingMore = require('trackingmore-sdk-nodejs')
    const key = 'your api key'
    const trackingmore = new TrackingMore(key)

    # Perform queries based on various conditions
    const params = [{
        'tracking_number': '92419999920412543483090901',
        'courier_code':'ups-mi'
    },{
      'tracking_number': '92419999920594513018295593',
      'courier_code':'ups-mi'
    }]
    trackingmore.trackings.batchCreateTrackings(params)
      .then(result => console.log(result))
      .catch(e => console.log(e))


Update a tracking by ID:

    const TrackingMore = require('trackingmore-sdk-nodejs')
    const key = 'your api key'
    const trackingmore = new TrackingMore(key)
    
    const params = {
        'customer_name': 'New name',
        'note':'New test order note'
    }
    const idString = "9dc04fc69689eaa1eadd65882ca66857"
    trackingmore.trackings.updateTrackingByID(idString, params)
      .then(result => console.log(result))
      .catch(e => console.log(e))
