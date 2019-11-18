var geojson;
    $(document).ready(function () {
        $.getJSON("urlWhereIretrieveTheJson", function (geoJson) {
            geojson = L.geoJson(geoJson, { style: style, onEachFeature: onEachFeature }).addTo(map);

            var sliderControl = L.control.sliderControl({
                position: "bottomleft",
                layer: geojson,
                range: false,
                showAllOnStart: false
            });

            map.addControl(sliderControl);
            sliderControl.startSlider();
            ;
        });
    });
the json schema is like the following:

{"type": "FeatureCollection",
"features": [
{"type":"Feature",
"properties": {"name": "Thies","bl": 6,"**time**": "**2013-01-01 00:00:00+00**"},
"geometry":{"type":"Polygon","coordinates":[....]} 
},{....}
]}
Here is a jsFiddle with complete code and datasource: http://jsfiddle.net/brainsengineering/nboo4ksg/

jquery-ui dictionary slider gis leaflet
shareimprove this question
edited Jun 8 '15 at 10:24

Jonatas Walker
9,59955 gold badges2929 silver badges6969 bronze badges
asked Jun 6 '15 at 11:30

Giox
1,95111 gold badge1414 silver badges3535 bronze badges
any chance of being able to throw this entire setup onto a demo site? – snkashis Jun 6 '15 at 18:40
@snkashis updated with jsFiddle – Giox Jun 8 '15 at 7:54
add a comment
1 Answer
active oldest votes

2

The answer to one thing that

I get also all the polygons (30) designed on top of each other, even if I specify "showAllOnStart: false"

is that you're adding geojson this way

geojson = L.geoJson(geoJson, { style: style, onEachFeature: onEachFeature }).addTo(map);
don't add addTo(map) at the end, simply do this

geojson = L.geoJson(geoJson, { style: style, onEachFeature: onEachFeature });
the other thing is that you want to group your data based on same values i.e group data for year 2013, 2014 and 2015. For this we need to alter the plugin a bit because currently the plugin don't handle to group data based on same values. So here is the code

L.Control.SliderControl = L.Control.extend({
options: {
    position: 'topright',
    layers: null,
    timeAttribute: 'time',
    isEpoch: false,     // whether the time attribute is seconds elapsed from epoch
    startTimeIdx: 0,    // where to start looking for a timestring
    timeStrLength: 19,  // the size of  yyyy-mm-dd hh:mm:ss - if millis are present this will be larger
    maxValue: -1,
    minValue: -1,
    showAllOnStart: false,
    markers: null,
    range: false,
    follow: false,
    alwaysShowDate : false,
    rezoom: null
},

initialize: function (options) {
    L.Util.setOptions(this, options);
    this._layer = this.options.layer;

},

extractTimestamp: function(time, options) {
    if (options.isEpoch) {
        time = (new Date(parseInt(time))).toString(); // this is local time
    }
    return time.substr(options.startTimeIdx, options.startTimeIdx + options.timeStrLength);
},

setPosition: function (position) {
    var map = this._map;

    if (map) {
        map.removeControl(this);
    }

    this.options.position = position;

    if (map) {
        map.addControl(this);
    }
    this.startSlider();
    return this;
},

onAdd: function (map) {
    this.options.map = map;

    // Create a control sliderContainer with a jquery ui slider
    var sliderContainer = L.DomUtil.create('div', 'slider', this._container);
    $(sliderContainer).append('<div id="leaflet-slider" style="width:200px"><div class="ui-slider-handle"></div><div id="slider-timestamp" style="width:200px; margin-top:13px; background-color:#FFFFFF; text-align:center; border-radius:5px;"></div></div>');
    //Prevent map panning/zooming while using the slider
    $(sliderContainer).mousedown(function () {
        map.dragging.disable();
    });
    $(document).mouseup(function () {
        map.dragging.enable();
        //Hide the slider timestamp if not range and option alwaysShowDate is set on false
        if (options.range || !options.alwaysShowDate) {
            $('#slider-timestamp').html('');
        }
    });

    var options = this.options;
    this.options.markers = [];
    this.options.unique_time_values = [];

    //If a layer has been provided: calculate the min and max values for the slider
    if (this._layer) {
        /*var index_temp = 0;
        this._layer.eachLayer(function (layer) {
            //console.log(layer);
            options.markers[index_temp] = layer;
            ++index_temp;
        });
        options.maxValue = index_temp - 1;
        this.options = options;*/

        var flags = [], unique_values = [],len;
        this._layer.eachLayer(function (layer) {

            if( flags[layer.feature.properties.time]) return;
            flags[layer.feature.properties.time] = true;
            unique_values.push(layer.feature.properties.time);
            ++len;

        });
        //console.log(unique_values);

        var all_features = [];
        for (var i=0;i<unique_values.length;i++){
            all_features[i] = [];
        }
        //console.log(all_features);

        //console.log(this._layer.getLayers().length)
        var layers = this._layer.getLayers()
        for(var i=0;i<layers.length;i++){

            //console.log(layers[i].feature.properties.time);
            var index = unique_values.indexOf(layers[i].feature.properties.time)
            //console.log(index);
            all_features[index].push(layers[i]);

        }
        //console.log(all_features);

        for (var i=0;i<all_features.length;i++){
            options.markers[i] = L.featureGroup(all_features[i]);
        }
        options.maxValue = all_features.length - 1;
        this.options = options;
        this.options.unique_time_values = unique_values

    } else {
        console.log("Error: You have to specify a layer via new SliderControl({layer: your_layer});");
    }
    return sliderContainer;
},

onRemove: function (map) {
    //Delete all markers which where added via the slider and remove the slider div
    for (i = this.options.minValue; i < this.options.maxValue; i++) {
        map.removeLayer(this.options.markers[i]);
    }
    $('#leaflet-slider').remove();
},

startSlider: function () {
    _options = this.options;
    _extractTimestamp = this.extractTimestamp
    var index_start = _options.minValue;
    if(_options.showAllOnStart){
        index_start = _options.maxValue;
        if(_options.range) _options.values = [_options.minValue,_options.maxValue];
        else _options.value = _options.maxValue;
    }
    $("#leaflet-slider").slider({
        range: _options.range,
        value: _options.minValue,
        values: _options.values,
        min: _options.minValue,
        max: _options.maxValue,
        step: 1,
        slide: function (e, ui) {
            var map = _options.map;
            var fg = L.featureGroup();
            if(!!_options.markers[ui.value]) {
                //console.log('inside');
                // If there is no time property, this line has to be removed (or exchanged with a different property)
                if(_options.markers[ui.value].feature !== undefined) {
                    if(_options.markers[ui.value].feature.properties[_options.timeAttribute]){
                        if(_options.markers[ui.value]) $('#slider-timestamp').html(
                            _extractTimestamp(_options.unique_values[ui.value].feature.properties[_options.timeAttribute], _options));
                    }else {
                        console.error("Time property "+ _options.timeAttribute +" not found in data");
                    }
                }else {
                    // set by leaflet Vector Layers
                    if(_options.unique_time_values[ui.value]){
                        if(_options.markers[ui.value]) $('#slider-timestamp').html(
                            _extractTimestamp(_options.unique_time_values[ui.value], _options));
                    }else {
                        console.error("Time property "+ _options.timeAttribute +" not found in data");
                    }
                }

                var i;
                // clear markers
                for (i = _options.minValue+1; i <= _options.maxValue; i++) {
                    if(_options.markers[i]) map.removeLayer(_options.markers[i]); 
                }
                if(_options.range){
                    // jquery ui using range
                    for (i = ui.values[0]; i <= ui.values[1]; i++){
                       if(_options.markers[i]) {
                           map.addLayer(_options.markers[i]);
                           fg.addLayer(_options.markers[i]);
                       }
                    }
                }else if(_options.follow){
                    for (i = ui.value - _options.follow + 1; i <= ui.value ; i++) {
                        if(_options.markers[i]) {
                            map.addLayer(_options.markers[i]);
                            fg.addLayer(_options.markers[i]);
                        }
                    }
                }else{
                    for (i = _options.minValue; i <= ui.value ; i++) {
                        if(_options.markers[i]) {
                            map.addLayer(_options.markers[i]);
                            fg.addLayer(_options.markers[i]);
                        }
                    }
                }
            };
            if(_options.rezoom) {
                map.fitBounds(fg.getBounds(), {
                    maxZoom: _options.rezoom
                });
            }
        }
    });
    if (!_options.range && _options.alwaysShowDate) {
        $('#slider-timestamp').html(_extractTimeStamp(_options.markers[index_start].feature.properties[_options.timeAttribute], _options));
    }
    for (i = _options.minValue; i < index_start; i++) {
        _options.map.addLayer(_options.markers[i]);
    }
}
});

L.control.sliderControl = function (options) {
    return new L.Control.SliderControl(options);
};
