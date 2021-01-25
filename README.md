### Basic Home Assistant integration with ЛУН Місто

![Example](https://github.com/github/vitaliy-sk/lun-misto-home-assistant/blob/assets/screen.png)

```yml
sensor:
  - platform: rest
    name: Misto Lun
    resource: https://api.meteostation.online/chrome/addon/informer/
    value_template: '{{ value_json.lunmisto_air.aqi_scale_desc }}'
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
      aqi:
        friendly_name: 'AQI'
        value_template: '{{ states.sensor.misto_lun.attributes.lunmisto_air.aqi_scale_value | round(2) }}'
        unit_of_measurement: "μg/m³"
        icon_template: "mdi:weather-fog"
      jams:
        friendly_name: 'Jams'
        value_template: '{{ states.sensor.misto_lun.attributes.tomtom_jams.jams | round(2) }}'
        unit_of_measurement: "%"
        icon_template: "mdi:traffic-light"
```