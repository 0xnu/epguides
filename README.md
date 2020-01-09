# EPGuides

EPGuides - Electronic Program Guide - is a useful and straightforward tv program data covering countries across the globe. It's free to use, updated every seven days, and provides simple array access to the downloaded XML structures.

## EPG Data

Supports Belgium, France, Germany, and United Kingdom TV Channels at the moment:

 - **Belgium, France, Germany and United Kingdom (combined epg, but it is large):**
 	- XML Format: ```http://www.epgapi.ml/epg```

 - **Belgium:**
    - XML Format: ```http://www.epgapi.ml/be```

 - **France:**
 	- XML Format: ```http://www.epgapi.ml/fr```

 - **Germany:**
 	- XML Format: ```http://www.epgapi.ml/de```

 - **United Kingdom:**
 	- XML Format: ```http://www.epgapi.ml/uk```

## JSON Format

Need the EPG data in JSON format? You can parse the XML output asynchronously without the callback hell using xml2js. Don't forget to replace **epg** with **be**, **de**, **fr** or **uk** in the URL if you need it for a specific country.

```javascript
var eyes = require('eyes'),
    http = require('http'),
    async =require('async'),
    xml2js = require('xml2js');

async.waterfall([
    function(callback) {
        http.get('http://www.epgapi.ml/epg', function(res) {
            var response_data = '';
            res.setEncoding('utf8');
            res.on('data', function(chunk) {
                response_data += chunk;
            });
            res.on('end', function() {
                callback(null, response_data)
            });
            res.on('error', function(err) {
                callback(err);
            });
        });
    },
    function(xml, callback) {
        var parser = new xml2js.Parser();
        parser.parseString(xml, function(err, result) {
            if (err) {
                callback(err);
            } else {
                callback(null, result);
            }
        });
    },
    function(json, callback) {
        // do something usefull with the json
        eyes.inspect(json);
        callback();
    }
], function(err, result) {
    if (err) {
        console.log('Got error');
        console.log(err);
    } else {
        console.log('Done.');
    }
});
```

## Need a guide for your country, got issues or questions?

:sunglasses: :wave: [Email Me](mailto:oketunjifinbarrs@gmail.com)