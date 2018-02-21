# Ready For Nature

Checks for upcoming inclement weather and alerts you if you have doors or windows open.

This SmartThings app is a fork of [Ready for Rain](https://github.com/imbrianj/ready_for_rain), with the following enhancements:

* An option to check the hourly forecast instead of the whole day forecast, which is useful during days with changeable weather.
* The ability to send TTS alerts to a configured media speaker (devices with **capability.musicPlayer**)
* An option to check and alert on the Air Quality Index via the U.S. EPA [AirNow API](https://docs.airnowapi.org/).
* An option to check and alert on the pollen index via [Pollen.com](https://www.pollen.com/).

## Setup

1. Install the app into the IDE via GitHub integration (if you have this configured), or the via the old fashioned way of pasting the code into the **New SmartApp** > **From Code** window.
2. If you plan to use the Air Quality check, you will need to:
    1. [Request a free AirNow API key](https://docs.airnowapi.org/account/request/)
    2. [Log in](https://docs.airnowapi.org/login) to the AirNow API website.
    3. Visit any of the Web Services documentation pages (e.g. [Forecast by Zip Code](https://docs.airnowapi.org/forecastsbyzip/docs)) and look for **Your API Key:** in the top right of the page.
    
       It should be a string of hexadecimal characters in the format **XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX**. If you see your API key simply listed as GUEST, that's not it. The main AirNow Web Services index page currently has a bug that shows this as the key even when logged in. Try one of the subpages.
    
       Copy the key to the clipboard.
    4. Go to the SmartThings IDE > My SmartApps > Ready For Nature and click on **App Settings** in the top right.
    5. Click **Settings** and paste in your API key in the **Value** box next to **airNowKey**
3. Once installed into the IDE, add and configure for your hub via the SmartThings mobile app.

## Acknowledgements

* Special thanks to [imbrianj](https://github.com/imbrianj) for the original **Ready for Rain** SmartApp and to [motley74](https://github.com/motley74) for his contributions.
* Thanks to [arsaboo](https://github.com/arsaboo/) for sharing the method for querying the Pollen.com API methods in his HomeAssistant config.
* App icons provided courtesy of [WebHostFace](https://www.webhostface.com/blog/material-design-icons/).

## Air Quality Data Limitations

Data returned is subject to the [limitations of the AirNow API](https://docs.airnowapi.org/faq#reportingAreaForecasts). Some zipcodes will simply not have any data available, in which case you will never receive alerts based on air quality and you may see the message "Failed to retrieve valid air quality data from AirNow" in the live logging section of the IDE. You can test whether data is avaiable for your zipcode by testing it on the [AirNow API Query Tool](https://docs.airnowapi.org/ForecastsByZip/query). If the output for the **application/json** format is simply [], then no data is available. Your best bet is to try a neighboring zipcode. Look up your zipcode on http://maps.huge.info/zip.htm and try some of the other zipcodes near you.

In addition, this app will only act on air quality index (AQI) values below 2000. The AirNow API sometimes reports completely erroneous and very high values, so anything above 2000 will be ignored. Here's why the cut-off is at that level:

The [EPA's AQI categories](https://airnow.gov/index.cfm?action=aqi_brochure.index) work on a scale from 0-500. Anything above 300 categorized as **Hazardous**, and according to the EPA, such conditions are "extremely rare" in the US and "generally occur only during events such as forest fires".

Values above 500 are categorized as **Beyond Index**, but have occasionally been reported in extremely polluted areas of China, so they are technically possible. It therefore seems prudent to allow for extreme readings, but at the same time set an upper limit beyond which values are considered to be an error.

## Using Air Quality and Pollen data in other apps

If you are interested in accessing the AirNow air quality index and/or the pollen index data for use in other apps, you may be intersted in these standalone virtual device type handlers that expose the data for use in other apps such as [webCoRE](https://wiki.webcore.co/):

* [AirNow Virtual Sensor](https://github.com/jschlackman/AirNow)
* [Pollen Virtual Sensor](https://github.com/jschlackman/PollenThing)
