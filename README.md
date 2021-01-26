### Basic Home Assistant integration with ЛУН Місто

![Example](https://raw.githubusercontent.com/vitaliy-sk/lun-misto-home-assistant/master/screen.png)

```yml
sensor:
  - platform: rest
    name: Misto Lun
    resource: https://api.meteostation.online/chrome/addon/informer/
    value_template: 'OK'
    json_attributes:
      - lunmisto_air
      - tomtom_jams
      - tomtom_temp
  - platform: template
    sensors:
      pm25:
        friendly_name: 'PM25'
        value_template: '{{ states.sensor.misto_lun.attributes.lunmisto_air.pm25 | round(2) }}'
        unit_of_measurement: "μg/m³"
        icon_template: "mdi:weather-fog"
      quality:
        friendly_name: 'Air quality'
        value_template: '{{ states.sensor.misto_lun.attributes.lunmisto_air.aqi_scale_desc | round(0) }}'
        icon_template: "mdi:weather-fog"
      aqi:
        friendly_name: 'AQI'
        value_template: '{{ states.sensor.misto_lun.attributes.lunmisto_air.aqi_scale_value | round(0) }}'
        icon_template: "mdi:weather-fog"
      jams:
        friendly_name: 'Jams'
        value_template: '{{ states.sensor.misto_lun.attributes.tomtom_jams.jams | round(0) }}'
        icon_template: "mdi:traffic-light"
```