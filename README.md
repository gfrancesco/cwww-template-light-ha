# What's this?

It's a [template light](https://www.home-assistant.io/integrations/light.template) for [Home Assistant](https://www.home-assistant.io) (HA) to control cold-white / warm-white (`CWWW`) LED light strips. The template was created to overcome the limitations of the Shelly RGBW2 LED light controller but might also be useful for other LED controllers.

See [my blog post](https://www.fvg.io/blog/F49AAB/home-assistant-cwww-led-light-template) for more details and motivation.

# How to use

Two [input number](https://www.home-assistant.io/integrations/input_number) helpers keep the state of the LED strip light (brightness and color temperature).
The template embeds the behavior logic between the HA user interface and the LED controller.

The `ALL_CAPS` labels in the [instructions below](#instructions) and in the template file _must_ be replaced with your values.
Here's a description of the different labels to replace:

- `TEMPLATE_LIGHT_NAME` : the name used by HA to refer to the light
- `TEMPLATE_LIGHT_FRIENDLY_NAME` : a more descriptive name for the light
- `WARM_LIGHT_LINE` : the name of the HA entity that controls the _warm light_ LED line
- `COLD_LIGHT_LINE` : the name of the HA entity that controls the _cold light_ LED line
- `TEMPLATE_LIGHT_BRIGHTNESS` : the _input_number_ helper name for the light brightness
- `TEMPLATE_LIGHT_TEMPERATURE` : the _input_number_ helper name for the light color temperature

Example:

 `LABEL` | Value 
 --- | --- 
 `TEMPLATE_LIGHT_NAME` | kitchen_light
 `TEMPLATE_LIGHT_FRIENDLY_NAME` | Kitchen Top Light
 `WARM_LIGHT_LINE` | shelly_rgbw2_channel_1
 `COLD_LIGHT_LINE` | shelly_rgbw2_channel_2
 `TEMPLATE_LIGHT_BRIGHTNESS` | kitchen_light_brightness
 `TEMPLATE_LIGHT_TEMPERATURE` | kitchen_light_temperature
 
## Instructions

1. Create an `input_number` helper from HA with
   - name: `TEMPLATE_LIGHT_BRIGHTNESS`
   - min: **0**
   - max: **255**
   - step: **1**
2. Create an `input_number` helper from HA with
   - name: `TEMPLATE_LIGHT_TEMPERATURE`
   - min: **153**
   - max: **500**
   - step: **1**
3. Copy the `template_light_cwww.yaml` file or its content into your configuration files
4. Replace all the `ALL_CAPS` labels in the template file with your own values
5. Restart HA


# Limitations and improvements

- Template lights in HA still use `Mired` instead of `Kelvin` as a unit of measurement for color temperature. It looks like HA, as a platform, started to move to `Kelvin` in the latest releases. The template will need to be updated to use `Kelvin`, although I guess `Mired` will be kept for compatibility reasons.
- The calculation is performed assuming that the same `CW`/`WW` ratio, at any power level, would produce the same color temperature. This might not always be 100% accurate; however in my tests I didn't notice color shifts big enough to be considered problematic.
