# Home Assistant Color Helpers

Common **jinja** template **color helper** functions for [![Home Assistant](https://img.shields.io/badge/Home-Assistant-000?logo=HomeAssistant&logoColor=fff&labelColor=41BDF5&style=flat&color=rgba(108,204,247,1))](https://github.com/home-assistant)

- [RGB to HEX](#rgb-to-hex)
- [HEX to RGB](#hex-to-rgb)
- RGB to HS
- HS to RGB


## RGB to HEX

<details>
  <summary> 👈 example input — <b>returns <code>0000ff</code></b> </summary>
  
```jinja
{%- set r = 0 -%}
{%- set g = 0 -%}
{%- set b = 255 -%}
```

</details>

```jinja
{{ '%02x%02x%02x' | format(r, g, b) }}
```

## HEX to RGB

<details>
  <summary> 👈 example input — <b>returns <code>(0, 0, 255)</code></b> </summary>
  
```jinja
{%- set rr = 'ff' -%}
{%- set gg = '00' -%}
{%- set bb = '00' -%}
```

</details>

```jinja
{{r | int(base=16), g | int(base=16), b | int(base=16)}}
```

### Get colors
```jinja
{{ states.light.reading.attributes.hs_color }}
# returns `(28.391, 65.659)`
```

```jinja
{{ states.light.reading.attributes.rgb_color }}
# returns `(255, 166, 87)`
```


## 🫵 Try them out in 

[![Open your Home Assistant instance and show your template developer tools.](https://my.home-assistant.io/badges/developer_template.svg)](https://my.home-assistant.io/redirect/developer_template/)
