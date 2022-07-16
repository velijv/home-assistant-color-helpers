# Home Assistant Color Helpers

Common **jinja** template **color helper** functions for [![Home Assistant](https://img.shields.io/badge/Home-Assistant-555?logo=HomeAssistant&logoColor=fff&labelColor=03a9f4&style=flat)](https://github.com/home-assistant)

2. convert [RGB to HEX](#rgb-to-hex)
3. convert [HEX to RGB](#hex-to-rgb)
5. convert [HS to RGB](#hs-to-rgb)
5. convert [HS to HEX](#hs-to-hex)
4. [~~convert RGB to HS~~](#home-assistant-color-helpers)

### Extract colors

<details>
  <summary> 🖖 Hue and Saturation <code>(state_attr('light.x','hs_color')</code> </summary>

```jinja
{%- set h = (state_attr('light.desk','hs_color') | list )[0] -%}
  # hue: {{ h }}
{%- set s = (state_attr('light.desk','hs_color') | list )[1] -%}
  # saturation: {{ s }}
```

</details>


<details>
  <summary> 🖐 Red, Green and Blue <code>state_attr('light.x','rgb_color')</code> </summary>

```jinja
{%- set r = (state_attr('light.desk','rgb_color') | list )[0] -%}
  # red: {{ r }}
{%- set g = (state_attr('light.desk','rgb_color') | list )[1] -%}
  # green: {{ g }}
{%- set b = (state_attr('light.desk','rgb_color') | list )[2] -%}
  # blue: {{ b }}
```

</details>

### Convert colors in Jinja template

## RGB to HEX

<details>
  <summary> 👈 example input <code>(0,0,255)</code> — <b>returns <code>0000ff</code></b> </summary>
  
```jinja
{%- set r = 0 -%}
{%- set g = 0 -%}
{%- set b = 255 -%}
```

</details>

> ```jinja
> hex: {{ '%02x%02x%02x' | format(r, g, b) }} - or - {{'%02x'%r+'%02x'%g+'%02x'%b}} 
> ```

## HEX to RGB

<details>
  <summary> 👈 example input <code>ff0000</code> — <b>returns <code>(255, 0, 0)</code></b> </summary>
  
```jinja
{%- set rr = 'ff' -%}
{%- set gg = '00' -%}
{%- set bb = '00' -%}
```

</details>

> ```jinja
> rgb: {{r | int(base=16), g | int(base=16), b | int(base=16)}}
> ```

## HS to RGB [![](https://img.shields.io/badge/🔥-🔫%20😡-B41717.svg?logo=jinja&logoColor=fff&labelColor=B41717&style=flat&color=rgba(180,23,23,0.3) "das f*kged up")](https://www.youtube.com/watch?v=MUx9BEu0ww0) [![](https://img.shields.io/github/sponsors/velijv?logo=githubsponsors&label=🥺&style=flat&labelColor=ff1493&logoColor=fff&color=rgba(234,74,170,0.5) "uwu papi-san")](https://github.com/sponsors/velijv)

<details>
  <summary> 👈 example input <code>hsv(240,100,100)</code> — <b>returns <code>(0, 0, 255)</code></b> </summary>
  
```jinja
{%- set h = (state_attr('light.desk','hs_color') | list )[0]  -%}
{%- set s = 100 -%}
{%- set v = (state_attr('light.desk','hs_color') | list )[1] -%} 
```

***

**`s` stays at `100`**. Because you only get 2 values from light in HA. An 🕯️ emitting light does not have *saturation*, it has 🔆 **brightness**.

</details>



<blockquote>
<details>
  <summary> <h3> 👉 <b>hs_color(h,s) -> rgb: {{ (r, g, b) | list }}</b> 👈 </h3> </summary>

```jinja
{%- set h = 360 -%}
{%- set s = 100 -%}
{%- set v = 100 -%}
{%- set i = (h * 6 ) | round(2,'floor') -%}
{%- set f = h * 6  - i  -%}
{%- set p = v * (1 - s) -%}
{%- set q = v * (1 - f * s) -%}
{%- set t = v * (1 - (1 - f) * s) -%}
{%- if i % 6 == 0 -%}
  {%- set r = v | int -%}
  {%- set g = t | int -%} 
  {%- set b = p | int -%}
{%- elif i % 6 == 1 -%}
  {%- set r = q | int -%}
  {%- set g = v | int -%}
  {%- set b = p | int -%}
{%- elif i % 6 == 2 -%}
  {%- set r = p | int -%}
  {%- set g = v | int -%}
  {%- set b = t | int -%}
{%- elif i % 6 == 3 -%}
  {%- set r = p | int -%}
  {%- set g = q | int -%}
  {%- set b = v | int -%}
{%- elif i % 6 == 4 -%}
  {%- set r = t | int -%}
  {%- set g = p | int -%}
  {%- set b = v | int -%}
{%- elif i % 6 == 5 -%}
  {%- set r = v | int -%}
  {%- set g = p | int -%}
  {%- set b = q | int -%}
{%- endif -%}

rgb: {{ (r, g, b) | list }}
```

</details>
</blockquote>

## [HS to HEX](#rgb-to-hex)

***

### Try them out in [![Open your Home Assistant instance and show your template developer tools.](https://img.shields.io/badge/My%20🫵-Template%20Dev%20Tools%20🥷-555?logo=HomeAssistant&logoColor=fff&labelColor=555&style=flat&color=03a9f4)](https://my.home-assistant.io/redirect/developer_template/) [![uwu](https://img.shields.io/github/sponsors/velijv?logo=githubsponsors&label=🫠&style=flat-square&labelColor=rgba(0,0,0,0)&color=rgba(234,74,170,0.5) "for jsut 1 doolar you can lead a por man to fish")](https://github.com/sponsors/velijv) 
