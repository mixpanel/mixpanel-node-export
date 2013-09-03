MixpanelAPI
===========

Queries the [Mixpanel Data API](http://mixpanel.com/api/docs/guides/api/v2).
Requires node 0.8.0 or higher.

Installation
============
Clone this repo; it is not on npm yet. Then, run `npm install` from the top
directory to install the module dependencies.

Show me the code
================

Note: this was forked from the CoffeScript implementation done by Campfire Labs.

    mixpanel = require('mixpanel')

    var api_key = 'YOUR API KEY',
        api_secret = 'YOUR API SECRET';

    var mx = new mixpanel({
        api_key: api_key,
        api_secret: api_secret
    });

    mx.request(
        'button click',
        {
            type: 'unique',
            interval: 7,
            unit: 'day'
        },
        function(error, data) {
            console.dir(data);
        }
            
    )

Exporting raw data from Mixpanel
--------------------------------

Mixpanel provides a [raw data export API](https://mixpanel.com/docs/api-documentation/exporting-raw-data-you-inserted-into-mixpanel)
to dump raw events.

This can be called through the `export_data` method. This takes a callback that
receives a Node.js Readable Stream. By listening to the `data` event on this
stream, you receive individual event objects, one at a time.

    mixpanel = require('mixpanel');

    var api_key = 'YOUR API KEY',
        api_secret = 'YOUR API SECRET';

    var mx = new mixpanel({
        api_key: api_key,
        api_secret: api_secret
    });

    mx.export_data(function(res) {
        res.on('data', function(event_object) {
            console.dir(event_object);
        });
        res.on('end', function() {
            console.log('All events have been retrieved');
        });
    });

