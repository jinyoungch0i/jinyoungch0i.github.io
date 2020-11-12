---
layout: post
title:  "On Application"
date:   2020-11-08 06:05:11 -0500
category: journey
---

Perhaps my favourite aspect of computer programming is the ability to immediately apply my knowledge onto real-life projects, à la web. 

If you were a, say, biomedical researcher or a mechanical engineer, you would require some kind of physical infrastructure (in the form of a medical laboratory or a machine shop) in order to incubate and materialise your craft. 

Even outside the realm of STEM, if you work in finance or international development, you may be pressed on things like capital or fundraising.

In other words, your ideas are bound by the constraints of the physical world. 

As a counter perspective, it often amazes me how unhindered the field of software engineering is when it comes to the act of creating, much less the idea of deploying an individual creation to a wide-reaching platform like the internet.

All you need is a text editor/IDE, internet connection, and some programming language(s) and frameworks to structure and consolidate your thoughts onto the computer's logic. 

Despite the growing pains that come from the never-ending quest for knowledge, I have gotten to appreciate how one can straight away apply their newfound knowledge onto a tangible creation. 

For instance, I finally learned how to work with APIs and applied my findings to this website.

The idea was to work with [OpenWeatherMap](https://openweathermap.org/){:target="_blank"}, whose API provides realtime weather information that corresponds to the client location (i.e. where the site visitor is connecting from). 

Incorporating the ```<APIKey>```, I firstly pulled some data from OpenWeatherMap by calling its API:
```javascript
function getWeather(lat, lng) {
    fetch(
        `https://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lng}&appid=<APIKey>&units=metric`
    )
    .then(function(response) {
        return response.json();
    })
```
And the data was received in the following JSON format:  
```json
{"coord":{"lon":-82.6,"lat":35.57},"weather":[{"id":701,"main":"Mist","description":"mist","icon":"50d"}],"base":"stations","main":{"temp":21.28,"feels_like":24.14,"temp_min":19.44,"temp_max":22.78,"pressure":1016,"humidity":100},"visibility":6437,"wind":{"speed":2.1,"deg":160},"clouds":{"all":90},"dt":1605118449,"sys":{"type":1,"id":3351,"country":"US","sunrise":1605096159,"sunset":1605133589},"timezone":-18000,"id":4453066,"name":"Asheville","cod":200}
```
After that, I cheerypicked a few datapoints, such as ```temp``` and ```name```, and assigned them into variables ```temperature``` and ```place```. I also made a fahrenheit conversion and assigned it to ```temperature_murica```:
```javascript
    .then(function(json) {
        const temperature = json.main.temp.toFixed(0); //celsius, rounded up
        const place = json.name.toLowerCase(); //lowercase for consistency
        const temperature_murica = ((temperature * 9/5) + 32).toFixed(0); //fahrenheit conversion
```
I then wrote in a JavaScript template literal-- with the aforemetioned variables put in ${placeholders}-- which will be the format of the weather info. displayed:
```javascript
weather.innerText = `${temperature}°c / ${temperature_murica}°f in ${place}`;
```
Lastly, with the JavaScript code written, the only thing that was left was to tie together this logic to the HTML backbone:
```html
<span id="weather"></span>
<script src="./assets/js/weather.js" type="text/javascript" defer ></script>
```

And voilá!

As a visitor accessing [jinyoung.xyz](https://www.jinyoung.xyz/){:target='_blank'}, you will first be prompted to grant location access (as per your browser's security protocol) and, once granted, will display a line of weather information for your location, right below the navigation bar:

[click here for a demo](https://photos.app.goo.gl/8kr3GXo6o678zju59){:target="_blank"}

Looking back, the past month of learning JavaScript has been the toughest personal learning curve in my programming journey (more on this in my previous entry, [On Patience](https://www.jinyoung.xyz/journey/2020/10/23/on-patience.html){:target="_blank"}).

However, I cannot be more excited at just how much more I'll be able to do with programing in the months to come. 

I'm starting to like JavaScript! :)

