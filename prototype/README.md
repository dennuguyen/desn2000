# Prototype 🧱

Building a proof-of-concept.

## Work Packages 💼

[TOC]

- System design.
- Cycle of analysis, CAD, simulation.
- Verify solution works (through analysis and simulation).
- Validate solution against requirements.

## Requirements Allocation 🔑

The requirements to consider for system design were:
- `FR(1.1.1.1)`: Withstand turbulent airflow where Reynolds number ranges from $30000 - 60000$.
- `FR(1.1.1.3)`: Able to operate in air flow between $1400 - 1600 \space L/s$.
- `FR(1.1.1.4)`: Able to operate in speeds between $3 - 5 \space m/s$.
- `FR(1.1.1.5)`: Harvest wind energy with minimal noise pollution.
- `FR(1.3.1)`: Can power electronics at an average power of $3 \space W$.
- `FR(3.1)`: Detect particulates in air.
- `FR(3.2)`: Communicate data.

A requirements allocation was performed to identify the top-level subsystems:

```mermaid
graph LR
FR1.1.1.1 --> Funnel
FR1.1.1.3 --> Funnel
FR1.1.1.3 --> Turbine
FR1.1.1.4 --> Turbine
FR1.1.1.5 --> Dampers
FR1.3.1 --> Generator
FR1.3.1 --> Battery
FR3.1 --> Sensors
FR3.1 --> Control
FR3.2 --> Control
```

## Maximum Extractable Power ✈

Consider the maximum power that can be extracted from the fluid:
$$
P_{\text{fluid}} = \frac{1}{2} \rho A v^3
$$

Where:
- $P_{\text{fluid}} \space (W)$ is the power of the fluid.
- $rho \space (kg/m^3)$ is the fluid density.
- $A \space (m^2)$ is the cross-sectional surface area that the fluid flows.
- $v \space (m/s)$ is the fluid velocity.

The [range of the fluid velocity](https://www.engineeringtoolbox.com/flow-velocity-air-ducts-d_388.html) is:
$$
\begin{aligned}
v_{\text{min}} &= 5 \space m/s \\
v_{\text{max}} &= 11 \space m/s
\end{aligned}
$$

The fluid density of air is:
$$
\rho = 1.225 \space kg/m^3
$$

Referring to this table of [common rectangular ducts](https://www.engineeringtoolbox.com/rectangular-ducts-d_1010.html), a table of maximum extractable fluid power vs air duct size is created:

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  overflow:hidden;padding:10px 5px;word-break:normal;}
.tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  font-weight:normal;overflow:hidden;padding:10px 5px;word-break:normal;}
.tg .tg-ak90{background-color:#ED9570;text-align:center;vertical-align:bottom}
.tg .tg-uklj{background-color:#EBD36A;text-align:center;vertical-align:bottom}
.tg .tg-g1b3{background-color:#FBD667;text-align:center;vertical-align:bottom}
.tg .tg-a2dl{background-color:#E67C73;text-align:center;vertical-align:bottom}
.tg .tg-zy3w{background-color:#DFD16C;text-align:center;vertical-align:bottom}
.tg .tg-i74i{background-color:#FDCF67;text-align:center;vertical-align:bottom}
.tg .tg-bobw{font-weight:bold;text-align:center;vertical-align:bottom}
.tg .tg-saxo{background-color:#B1CA76;text-align:center;vertical-align:bottom}
.tg .tg-odu0{background-color:#ECD36A;text-align:center;vertical-align:bottom}
.tg .tg-wim9{background-color:#C8CE71;text-align:center;vertical-align:bottom}
.tg .tg-iymw{background-color:#D0CF70;text-align:center;vertical-align:bottom}
.tg .tg-ucbw{background-color:#DED16D;text-align:center;vertical-align:bottom}
.tg .tg-5xxj{background-color:#91C57D;text-align:center;vertical-align:bottom}
.tg .tg-la2o{background-color:#EC9270;text-align:center;vertical-align:bottom}
.tg .tg-evjp{background-color:#EB8F71;text-align:center;vertical-align:bottom}
.tg .tg-h0jm{background-color:#F2A96D;text-align:center;vertical-align:bottom}
.tg .tg-pw7g{background-color:#EF9D6F;text-align:center;vertical-align:bottom}
.tg .tg-n8yn{background-color:#F6B56B;text-align:center;vertical-align:bottom}
.tg .tg-99k1{background-color:#FED666;text-align:center;vertical-align:bottom}
.tg .tg-1goq{background-color:#F0A26E;text-align:center;vertical-align:bottom}
.tg .tg-uk67{background-color:#E98872;text-align:center;vertical-align:bottom}
.tg .tg-f0bb{background-color:#E78173;text-align:center;vertical-align:bottom}
.tg .tg-o3vm{background-color:#B7CB75;text-align:center;vertical-align:bottom}
.tg .tg-zph9{background-color:#6BBF85;text-align:center;vertical-align:bottom}
.tg .tg-qx7g{background-color:#D4D06F;text-align:center;vertical-align:bottom}
.tg .tg-32si{background-color:#FFD666;text-align:center;vertical-align:bottom}
.tg .tg-1qvh{background-color:#97C67C;text-align:center;vertical-align:bottom}
.tg .tg-7wv7{background-color:#F6B96B;text-align:center;vertical-align:bottom}
.tg .tg-bxtm{background-color:#A4C879;text-align:center;vertical-align:bottom}
.tg .tg-rk9c{background-color:#F4AF6C;text-align:center;vertical-align:bottom}
.tg .tg-kdq1{background-color:#E4D26B;text-align:center;vertical-align:bottom}
.tg .tg-9ywq{background-color:#C1CC73;text-align:center;vertical-align:bottom}
.tg .tg-amwm{font-weight:bold;text-align:center;vertical-align:top}
.tg .tg-ugok{background-color:#E67F73;text-align:center;vertical-align:bottom}
.tg .tg-zup4{background-color:#E78273;text-align:center;vertical-align:bottom}
.tg .tg-yrz9{background-color:#E88572;text-align:center;vertical-align:bottom}
.tg .tg-t3zq{background-color:#EE9C6F;text-align:center;vertical-align:bottom}
.tg .tg-wj4b{background-color:#F9C269;text-align:center;vertical-align:bottom}
.tg .tg-4smu{background-color:#E67D73;text-align:center;vertical-align:bottom}
.tg .tg-kau8{background-color:#E98972;text-align:center;vertical-align:bottom}
.tg .tg-p9n2{background-color:#EA8D71;text-align:center;vertical-align:bottom}
.tg .tg-xglf{background-color:#F1A56D;text-align:center;vertical-align:bottom}
.tg .tg-im9s{background-color:#FAC569;text-align:center;vertical-align:bottom}
.tg .tg-jwyu{background-color:#E88472;text-align:center;vertical-align:bottom}
.tg .tg-4zal{background-color:#F7D567;text-align:center;vertical-align:bottom}
.tg .tg-cks2{background-color:#F1D469;text-align:center;vertical-align:bottom}
.tg .tg-6e0j{background-color:#F0D469;text-align:center;vertical-align:bottom}
.tg .tg-nabm{background-color:#E8D36B;text-align:center;vertical-align:bottom}
.tg .tg-jwiq{background-color:#D7D06E;text-align:center;vertical-align:bottom}
.tg .tg-1gz9{background-color:#CBCE71;text-align:center;vertical-align:bottom}
.tg .tg-ecwx{background-color:#FCD666;text-align:center;vertical-align:bottom}
.tg .tg-al2l{background-color:#F6D568;text-align:center;vertical-align:bottom}
.tg .tg-1p8w{background-color:#BECC74;text-align:center;vertical-align:bottom}
.tg .tg-52o3{background-color:#A8C878;text-align:center;vertical-align:bottom}
.tg .tg-2zh6{background-color:#7EC281;text-align:center;vertical-align:bottom}
.tg .tg-mxkh{background-color:#FCCC68;text-align:center;vertical-align:bottom}
.tg .tg-y7jj{background-color:#F4D568;text-align:center;vertical-align:bottom}
.tg .tg-542a{background-color:#87C37F;text-align:center;vertical-align:bottom}
.tg .tg-z7mu{background-color:#78C183;text-align:center;vertical-align:bottom}
.tg .tg-yew5{background-color:#57BB8A;text-align:center;vertical-align:bottom}
</style>
<table class="tg">
<thead>
  <tr>
    <th class="tg-amwm" rowspan="2">Width (mm)</th>
    <th class="tg-bobw" colspan="11"><span style="font-weight:bold">Height (mm)</span></th>
  </tr>
  <tr>
    <th class="tg-bobw"><span style="font-weight:bold">100</span></th>
    <th class="tg-bobw"><span style="font-weight:bold">150</span></th>
    <th class="tg-bobw"><span style="font-weight:bold">200</span></th>
    <th class="tg-bobw"><span style="font-weight:bold">250</span></th>
    <th class="tg-bobw"><span style="font-weight:bold">300</span></th>
    <th class="tg-bobw"><span style="font-weight:bold">400</span></th>
    <th class="tg-bobw"><span style="font-weight:bold">500</span></th>
    <th class="tg-bobw"><span style="font-weight:bold">600</span></th>
    <th class="tg-bobw"><span style="font-weight:bold">800</span></th>
    <th class="tg-bobw"><span style="font-weight:bold">1000</span></th>
    <th class="tg-bobw"><span style="font-weight:bold">1200</span></th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-bobw"><span style="font-weight:bold">200</span></td>
    <td class="tg-a2dl"><span style="font-weight:normal;background-color:#E67C73">1.53</span></td>
    <td class="tg-ugok"><span style="font-weight:normal;background-color:#E67F73">2.30</span></td>
    <td class="tg-zup4"><span style="font-weight:normal;background-color:#E78273">3.06</span></td>
    <td class="tg-yrz9"><span style="font-weight:normal;background-color:#E88572">3.83</span></td>
    <td class="tg-uk67"><span style="font-weight:normal;background-color:#E98872">4.59</span></td>
    <td class="tg-evjp"><span style="font-weight:normal;background-color:#EB8F71">6.13</span></td>
    <td class="tg-ak90"><span style="font-weight:normal;background-color:#ED9570">7.66</span></td>
    <td class="tg-t3zq"><span style="font-weight:normal;background-color:#EE9C6F">9.19</span></td>
    <td class="tg-h0jm"><span style="font-weight:normal;background-color:#F2A96D">12.25</span></td>
    <td class="tg-n8yn"><span style="font-weight:normal;background-color:#F6B56B">15.31</span></td>
    <td class="tg-wj4b"><span style="font-weight:normal;background-color:#F9C269">18.38</span></td>
  </tr>
  <tr>
    <td class="tg-bobw"><span style="font-weight:bold">250</span></td>
    <td class="tg-4smu"><span style="font-weight:normal;background-color:#E67D73">1.91</span></td>
    <td class="tg-f0bb"><span style="font-weight:normal;background-color:#E78173">2.87</span></td>
    <td class="tg-yrz9"><span style="font-weight:normal;background-color:#E88572">3.83</span></td>
    <td class="tg-kau8"><span style="font-weight:normal;background-color:#E98972">4.79</span></td>
    <td class="tg-p9n2"><span style="font-weight:normal;background-color:#EA8D71">5.74</span></td>
    <td class="tg-ak90"><span style="font-weight:normal;background-color:#ED9570">7.66</span></td>
    <td class="tg-pw7g"><span style="font-weight:normal;background-color:#EF9D6F">9.57</span></td>
    <td class="tg-xglf"><span style="font-weight:normal;background-color:#F1A56D">11.48</span></td>
    <td class="tg-n8yn"><span style="font-weight:normal;background-color:#F6B56B">15.31</span></td>
    <td class="tg-im9s"><span style="font-weight:normal;background-color:#FAC569">19.14</span></td>
    <td class="tg-32si"><span style="font-weight:normal;background-color:#FFD666">22.97</span></td>
  </tr>
  <tr>
    <td class="tg-bobw"><span style="font-weight:bold">300</span></td>
    <td class="tg-ugok"><span style="font-weight:normal;background-color:#E67F73">2.30</span></td>
    <td class="tg-jwyu"><span style="font-weight:normal;background-color:#E88472">3.45</span></td>
    <td class="tg-uk67"><span style="font-weight:normal;background-color:#E98872">4.59</span></td>
    <td class="tg-p9n2"><span style="font-weight:normal;background-color:#EA8D71">5.74</span></td>
    <td class="tg-la2o"><span style="font-weight:normal;background-color:#EC9270">6.89</span></td>
    <td class="tg-t3zq"><span style="font-weight:normal;background-color:#EE9C6F">9.19</span></td>
    <td class="tg-xglf"><span style="font-weight:normal;background-color:#F1A56D">11.48</span></td>
    <td class="tg-rk9c"><span style="font-weight:normal;background-color:#F4AF6C">13.78</span></td>
    <td class="tg-wj4b"><span style="font-weight:normal;background-color:#F9C269">18.38</span></td>
    <td class="tg-32si"><span style="font-weight:normal;background-color:#FFD666">22.97</span></td>
    <td class="tg-g1b3"><span style="font-weight:normal;background-color:#FBD667">27.56</span></td>
  </tr>
  <tr>
    <td class="tg-bobw"><span style="font-weight:bold">400</span></td>
    <td class="tg-zup4"><span style="font-weight:normal;background-color:#E78273">3.06</span></td>
    <td class="tg-uk67"><span style="font-weight:normal;background-color:#E98872">4.59</span></td>
    <td class="tg-evjp"><span style="font-weight:normal;background-color:#EB8F71">6.13</span></td>
    <td class="tg-ak90"><span style="font-weight:normal;background-color:#ED9570">7.66</span></td>
    <td class="tg-t3zq"><span style="font-weight:normal;background-color:#EE9C6F">9.19</span></td>
    <td class="tg-h0jm"><span style="font-weight:normal;background-color:#F2A96D">12.25</span></td>
    <td class="tg-n8yn"><span style="font-weight:normal;background-color:#F6B56B">15.31</span></td>
    <td class="tg-wj4b"><span style="font-weight:normal;background-color:#F9C269">18.38</span></td>
    <td class="tg-99k1"><span style="font-weight:normal;background-color:#FED666">24.50</span></td>
    <td class="tg-4zal"><span style="font-weight:normal;background-color:#F7D567">30.63</span></td>
    <td class="tg-cks2"><span style="font-weight:normal;background-color:#F1D469">36.75</span></td>
  </tr>
  <tr>
    <td class="tg-bobw"><span style="font-weight:bold">500</span></td>
    <td class="tg-yrz9"><span style="font-weight:normal;background-color:#E88572">3.83</span></td>
    <td class="tg-p9n2"><span style="font-weight:normal;background-color:#EA8D71">5.74</span></td>
    <td class="tg-ak90"><span style="font-weight:normal;background-color:#ED9570">7.66</span></td>
    <td class="tg-pw7g"><span style="font-weight:normal;background-color:#EF9D6F">9.57</span></td>
    <td class="tg-xglf"><span style="font-weight:normal;background-color:#F1A56D">11.48</span></td>
    <td class="tg-n8yn"><span style="font-weight:normal;background-color:#F6B56B">15.31</span></td>
    <td class="tg-im9s"><span style="font-weight:normal;background-color:#FAC569">19.14</span></td>
    <td class="tg-32si"><span style="font-weight:normal;background-color:#FFD666">22.97</span></td>
    <td class="tg-4zal"><span style="font-weight:normal;background-color:#F7D567">30.63</span></td>
    <td class="tg-6e0j"><span style="font-weight:normal;background-color:#F0D469">38.28</span></td>
    <td class="tg-nabm"><span style="font-weight:normal;background-color:#E8D36B">45.94</span></td>
  </tr>
  <tr>
    <td class="tg-bobw"><span style="font-weight:bold">600</span></td>
    <td class="tg-uk67"><span style="font-weight:normal;background-color:#E98872">4.59</span></td>
    <td class="tg-la2o"><span style="font-weight:normal;background-color:#EC9270">6.89</span></td>
    <td class="tg-t3zq"><span style="font-weight:normal;background-color:#EE9C6F">9.19</span></td>
    <td class="tg-xglf"><span style="font-weight:normal;background-color:#F1A56D">11.48</span></td>
    <td class="tg-rk9c"><span style="font-weight:normal;background-color:#F4AF6C">13.78</span></td>
    <td class="tg-wj4b"><span style="font-weight:normal;background-color:#F9C269">18.38</span></td>
    <td class="tg-32si"><span style="font-weight:normal;background-color:#FFD666">22.97</span></td>
    <td class="tg-g1b3"><span style="font-weight:normal;background-color:#FBD667">27.56</span></td>
    <td class="tg-cks2"><span style="font-weight:normal;background-color:#F1D469">36.75</span></td>
    <td class="tg-nabm"><span style="font-weight:normal;background-color:#E8D36B">45.94</span></td>
    <td class="tg-ucbw"><span style="font-weight:normal;background-color:#DED16D">55.13</span></td>
  </tr>
  <tr>
    <td class="tg-bobw"><span style="font-weight:bold">800</span></td>
    <td class="tg-evjp"><span style="font-weight:normal;background-color:#EB8F71">6.13</span></td>
    <td class="tg-t3zq"><span style="font-weight:normal;background-color:#EE9C6F">9.19</span></td>
    <td class="tg-h0jm"><span style="font-weight:normal;background-color:#F2A96D">12.25</span></td>
    <td class="tg-n8yn"><span style="font-weight:normal;background-color:#F6B56B">15.31</span></td>
    <td class="tg-wj4b"><span style="font-weight:normal;background-color:#F9C269">18.38</span></td>
    <td class="tg-99k1"><span style="font-weight:normal;background-color:#FED666">24.50</span></td>
    <td class="tg-4zal"><span style="font-weight:normal;background-color:#F7D567">30.63</span></td>
    <td class="tg-cks2"><span style="font-weight:normal;background-color:#F1D469">36.75</span></td>
    <td class="tg-kdq1"><span style="font-weight:normal;background-color:#E4D26B">49.00</span></td>
    <td class="tg-jwiq"><span style="font-weight:normal;background-color:#D7D06E">61.25</span></td>
    <td class="tg-1gz9"><span style="font-weight:normal;background-color:#CBCE71">73.50</span></td>
  </tr>
  <tr>
    <td class="tg-bobw"><span style="font-weight:bold">1000</span></td>
    <td class="tg-ak90"><span style="font-weight:normal;background-color:#ED9570">7.66</span></td>
    <td class="tg-xglf"><span style="font-weight:normal;background-color:#F1A56D">11.48</span></td>
    <td class="tg-n8yn"><span style="font-weight:normal;background-color:#F6B56B">15.31</span></td>
    <td class="tg-im9s"><span style="font-weight:normal;background-color:#FAC569">19.14</span></td>
    <td class="tg-32si"><span style="font-weight:normal;background-color:#FFD666">22.97</span></td>
    <td class="tg-4zal"><span style="font-weight:normal;background-color:#F7D567">30.63</span></td>
    <td class="tg-6e0j"><span style="font-weight:normal;background-color:#F0D469">38.28</span></td>
    <td class="tg-nabm"><span style="font-weight:normal;background-color:#E8D36B">45.94</span></td>
    <td class="tg-jwiq"><span style="font-weight:normal;background-color:#D7D06E">61.25</span></td>
    <td class="tg-wim9"><span style="font-weight:normal;background-color:#C8CE71">76.56</span></td>
    <td class="tg-o3vm"><span style="font-weight:normal;background-color:#B7CB75">91.88</span></td>
  </tr>
  <tr>
    <td class="tg-bobw"><span style="font-weight:bold">1200</span></td>
    <td class="tg-t3zq"><span style="font-weight:normal;background-color:#EE9C6F">9.19</span></td>
    <td class="tg-rk9c"><span style="font-weight:normal;background-color:#F4AF6C">13.78</span></td>
    <td class="tg-wj4b"><span style="font-weight:normal;background-color:#F9C269">18.38</span></td>
    <td class="tg-32si"><span style="font-weight:normal;background-color:#FFD666">22.97</span></td>
    <td class="tg-g1b3"><span style="font-weight:normal;background-color:#FBD667">27.56</span></td>
    <td class="tg-cks2"><span style="font-weight:normal;background-color:#F1D469">36.75</span></td>
    <td class="tg-nabm"><span style="font-weight:normal;background-color:#E8D36B">45.94</span></td>
    <td class="tg-ucbw"><span style="font-weight:normal;background-color:#DED16D">55.13</span></td>
    <td class="tg-1gz9"><span style="font-weight:normal;background-color:#CBCE71">73.50</span></td>
    <td class="tg-o3vm"><span style="font-weight:normal;background-color:#B7CB75">91.88</span></td>
    <td class="tg-bxtm"><span style="font-weight:normal;background-color:#A4C879">110.25</span></td>
  </tr>
  <tr>
    <td class="tg-bobw"><span style="font-weight:bold">1400</span></td>
    <td class="tg-1goq"><span style="font-weight:normal;background-color:#F0A26E">10.72</span></td>
    <td class="tg-7wv7"><span style="font-weight:normal;background-color:#F6B96B">16.08</span></td>
    <td class="tg-i74i"><span style="font-weight:normal;background-color:#FDCF67">21.44</span></td>
    <td class="tg-ecwx"><span style="font-weight:normal;background-color:#FCD666">26.80</span></td>
    <td class="tg-al2l"><span style="font-weight:normal;background-color:#F6D568">32.16</span></td>
    <td class="tg-uklj"><span style="font-weight:normal;background-color:#EBD36A">42.88</span></td>
    <td class="tg-zy3w"><span style="font-weight:normal;background-color:#DFD16C">53.59</span></td>
    <td class="tg-qx7g"><span style="font-weight:normal;background-color:#D4D06F">64.31</span></td>
    <td class="tg-1p8w"><span style="font-weight:normal;background-color:#BECC74">85.75</span></td>
    <td class="tg-52o3"><span style="font-weight:normal;background-color:#A8C878">107.19</span></td>
    <td class="tg-5xxj"><span style="font-weight:normal;background-color:#91C57D">128.63</span></td>
  </tr>
  <tr>
    <td class="tg-bobw"><span style="font-weight:bold">1600</span></td>
    <td class="tg-h0jm"><span style="font-weight:normal;background-color:#F2A96D">12.25</span></td>
    <td class="tg-wj4b"><span style="font-weight:normal;background-color:#F9C269">18.38</span></td>
    <td class="tg-99k1"><span style="font-weight:normal;background-color:#FED666">24.50</span></td>
    <td class="tg-4zal"><span style="font-weight:normal;background-color:#F7D567">30.63</span></td>
    <td class="tg-cks2"><span style="font-weight:normal;background-color:#F1D469">36.75</span></td>
    <td class="tg-kdq1"><span style="font-weight:normal;background-color:#E4D26B">49.00</span></td>
    <td class="tg-jwiq"><span style="font-weight:normal;background-color:#D7D06E">61.25</span></td>
    <td class="tg-1gz9"><span style="font-weight:normal;background-color:#CBCE71">73.50</span></td>
    <td class="tg-saxo"><span style="font-weight:normal;background-color:#B1CA76">98.00</span></td>
    <td class="tg-1qvh"><span style="font-weight:normal;background-color:#97C67C">122.50</span></td>
    <td class="tg-2zh6"><span style="font-weight:normal;background-color:#7EC281">147.00</span></td>
  </tr>
  <tr>
    <td class="tg-bobw"><span style="font-weight:bold">1800</span></td>
    <td class="tg-rk9c"><span style="font-weight:normal;background-color:#F4AF6C">13.78</span></td>
    <td class="tg-mxkh"><span style="font-weight:normal;background-color:#FCCC68">20.67</span></td>
    <td class="tg-g1b3"><span style="font-weight:normal;background-color:#FBD667">27.56</span></td>
    <td class="tg-y7jj"><span style="font-weight:normal;background-color:#F4D568">34.45</span></td>
    <td class="tg-odu0"><span style="font-weight:normal;background-color:#ECD36A">41.34</span></td>
    <td class="tg-ucbw"><span style="font-weight:normal;background-color:#DED16D">55.13</span></td>
    <td class="tg-iymw"><span style="font-weight:normal;background-color:#D0CF70">68.91</span></td>
    <td class="tg-9ywq"><span style="font-weight:normal;background-color:#C1CC73">82.69</span></td>
    <td class="tg-bxtm"><span style="font-weight:normal;background-color:#A4C879">110.25</span></td>
    <td class="tg-542a"><span style="font-weight:normal;background-color:#87C37F">137.81</span></td>
    <td class="tg-zph9"><span style="font-weight:normal;background-color:#6BBF85">165.38</span></td>
  </tr>
  <tr>
    <td class="tg-bobw"><span style="font-weight:bold">2000</span></td>
    <td class="tg-n8yn"><span style="font-weight:normal;background-color:#F6B56B">15.31</span></td>
    <td class="tg-32si"><span style="font-weight:normal;background-color:#FFD666">22.97</span></td>
    <td class="tg-4zal"><span style="font-weight:normal;background-color:#F7D567">30.63</span></td>
    <td class="tg-6e0j"><span style="font-weight:normal;background-color:#F0D469">38.28</span></td>
    <td class="tg-nabm"><span style="font-weight:normal;background-color:#E8D36B">45.94</span></td>
    <td class="tg-jwiq"><span style="font-weight:normal;background-color:#D7D06E">61.25</span></td>
    <td class="tg-wim9"><span style="font-weight:normal;background-color:#C8CE71">76.56</span></td>
    <td class="tg-o3vm"><span style="font-weight:normal;background-color:#B7CB75">91.88</span></td>
    <td class="tg-1qvh"><span style="font-weight:normal;background-color:#97C67C">122.50</span></td>
    <td class="tg-z7mu"><span style="font-weight:normal;background-color:#78C183">153.13</span></td>
    <td class="tg-yew5"><span style="font-weight:normal;background-color:#57BB8A">183.75</span></td>
  </tr>
</tbody>
</table>

From the requirement of the turbine being operable in duct sizes of at least $400 \space mm \times 400 \space mm$

## Sensor Array Selection ⚡️

> Research on sensors in this [Google Sheet](https://docs.google.com/spreadsheets/d/1f3vsNErERXZ-9NdXlSl-dcCkEAP_58Zadz2kLJG4f4g/edit#gid=0).

## Mechatronic System Design

Consider a gross perspective of possible devices and their power ratings:

<table>
    <tr>
        <th>Device</th>
        <th>Description</th>
        <th>Input Voltage (V)</th>
        <th>Input Current (mA)</th>
    </tr>
    <tr>
        <td><a href="https://store.arduino.cc/products/arduino-nano">Arduino Nano</a></td>
        <td>Microcontroller.</td>
        <td>7 - 12</td>
        <td>20 - 200</td>
    </tr>
    <tr>
        <td><a href="https://docs.arduino.cc/hardware/uno-rev3">Arduino Uno</a></td>
        <td>Microcontroller.</td>
        <td>7 - 12</td>
        <td>50 - 200</td>
    </tr>
    <tr>
        <td><a href="https://www.raspberrypi.com/products/raspberry-pi-4-model-b/specifications/">Raspberry Pi 4</a></td>
        <td>Microcontroller.</td>
        <td>4 - 6</td>
        <td>> 3</td>
    </tr>
    <tr>
        <td><a href="https://en.wikipedia.org/wiki/USB#Low-power_and_high-power_devices">High-Power USB 3.0</a></td>
        <td>To power sensor device.</td>
        <td>5</td>
        <td>900</td>
    </tr>
    <tr>
        <td><a href="https://en.wikipedia.org/wiki/USB#Low-power_and_high-power_devices">USB-C</a></td>
        <td>To power sensor device.</td>
        <td>5</td>
        <td>1500</td>
    </tr>
    <tr>
        <td><a href="https://core-electronics.com.au/wifi-bee-esp8266.html">Wifi Bee ESP8266</a></td>
        <td>Wifi module.</td>
        <td>3.3</td>
        <td>240</td>
    </tr>
    <tr>
        <td><a href="https://core-electronics.com.au/raspberry-pi-pico-w-wireless-wifi.html">Raspberry Pi Pico W</a></td>
        <td>Wifi module.</td>
        <td>1.8 - 5.5</td>
        <td>90</td>
    </tr>
    <tr>
        <td><a href="https://core-electronics.com.au/tinypico-v2-usb-c.html">TinyPICO V2 USB-C</a></td>
        <td>Wifi module.</td>
        <td>1.8 - 5.5</td>
        <td>90</td>
    </tr>
</table>

> Note that a lot of electronic devices can be powered by USB-C.

Consider the formula for electrical power:
$$
P = VI
$$

Where:
- $P \space (W)$ is the power.
- $V \space (V)$ is the voltage.
- $I \space (A)$ is the current.

Power use can be summed from considering the voltage and current ratings of the devices:
$$
\begin{aligned}
P_{\text{net}} &= P_{\text{Arduino Nano}} + P_{\text{USB-C}} + P_{\text{TinyPICO}} \\
&= 7 \times 0.02 + 5 \times 1.5 + 2 \times 0.09 \\
&= 7.82 \space W
\end{aligned}
$$



## Battery Selection 🔋

Consider the battery-life formula:
$$
b = \frac{Q}{I}
$$

Where:
- $b \space (hr)$ is the battery life.
- $Q \space (Ahr)$ is the battery capacity.
- $I \space (A)$ is the current load.


Assume that a small microcontroller, wifi module, and three USB-C devices are powered by the battery, the peak current load would be:
$$
\begin{aligned}
I_{\text{peak}} = 200 + 200 + 1500 \times 3 = 4900 \space mA \approx 4.9 \space A
\end{aligned}
$$

For a desired battery life at the peak current load:
$$
b_{\text{peak}} = 1 \space hr
$$

> 1 hour was selected as the maximum time a routine inspection of air quality could be carried out for.

The desired battery capacity is therefore:
$$
\begin{aligned}
Q &= b_{\text{peak}} \times I_{\text{peak}} \\
&= 1 \times 4.9 \\
&= 4.9 \space Ahr
\end{aligned}
$$

The battery capacity is the standard capacity of most phone-charging powerbanks

In practice, the current load will not be peaked. The current load at rest would realistically be the current draw of the microcontroller:
$$
I_{\text{rest}} = 20 \space mA = 0.02 \space A
$$

> The current draw of a wifi module at rest is $20 \space \mu A$. The sensors may be turned off when not in use.

For a desired battery capacity of $4.9 \space Ahr$, this gives an average battery life of:
$$
b_{\text{rest}} = \frac{Q}{I_{\text{rest}}} = \frac{4.9}{0.02} = 24.5 \space hr
$$

Therefore, any rechargaeable battery that is capable of supplying at least $5 \space V$ and with a capacity of at least $4.9 \space Ahr$ is desired.

> If a battery has greater than $5 \space V$, then a voltage regulator can be used to step-down the voltage.

> If a battery has less than $5 \space V$, then multiple batteries can be placed in series to increase the voltage.

A table of appropriate batteries:
<table>
    <tr>
        <th>Battery</th>
        <th>Type</th>
        <th>Capacity (mAhr)</th>
        <th>Discharge Voltage (V)</th>
        <th>Charge Voltage (V)</th>
        <th>Discharge Rate (C-rate)</th>
        <th>Charge Rate (C-rate)</th>
        <th>Dimensions (mm^3)</th>
        <th>Cycles</th>
    </tr>
    <tr>
        <td><a href="https://www.alibaba.com/product-detail/KC-CE-Certified-Rechargeable-Lithium-Ion_62445223510.html">105075</a></td>
        <td>Lipo</td>
        <td>5000</td>
        <td>3.7</td>
        <td>4.2</td>
        <td>0.2</td>
        <td>0.2</td>
        <td>76 x 50 x 10</td>
        <td></td>
    </tr>
</table>

### Confirm Usability of 105075 Battery

For two 105075 batteries in series, the charging voltage would be $8.4 \space V$ and charge rate is $0.2 \space C$.

The battery life of a single 105075 battery is:
$$
t = \frac{1}{Cr} = \frac{1}{0.2} = 5 \space hr
$$
- $t \space (hr)$ is the battery life.
- $Cr \space (hr^{-1})$ is the C-rate.

Consider Peukert's Law to determine the desired discharge rate:

$$
C_{p} = I^{k}t
$$

Where:
- $C_{p} \space (Ahr)$ is the capacity at one-ampere discharge rate.
- $I \space (Ahr)$ is the actual discharge current.
- $t \space (hr)$ is the time to discharge the battery.
- $k$ is the Peukert constant.

To confirm there is sufficient current to power the system:
$$
\begin{aligned}
0.2 &= I^{1.2} \times 1 \\
I_{\text{max}} &= 8.827 \approx 8.8 \space A > 5 \space A
\end{aligned}
$$

> $k = 1.2$ is very modest for a lithium-ion polymer battery due to its "high" efficiency.

## Turbine Power 💨

> Recall: $P_{\text{fluid}} = \frac{1}{2} \rho A v^3$.

Let the 

Multiply $P_{\text{fluid}}$ by Betz's coefficient to get $P_{\text{turbine}}$


Consider the [extended Bernoulli equation](https://www.engineeringtoolbox.com/mechanical-energy-equation-d_614.html) for a turbine (in terms of energy per unit mass):
$$
E_{\text{pressure, in}} + E_{\text{velocity, in}} + E_{\text{elevation, in}} = E_{\text{pressure, out}} + E_{\text{velocity, out}} + E_{\text{elevation, elevation}} + E_{\text{shaft}} + E_{\text{loss}}
$$

Substituting the energies in terms of velocities and pressures gives:
$$
\frac{p_{\text{in}}}{\rho} + \frac{v_{\text{in}}^2}{2} + gh_{\text{in}} = \frac{p_{\text{out}}}{\rho} + \frac{v_{\text{out}}^2}{2} + gh_{\text{out}} + E_{\text{shaft}} + E_{\text{loss}}
$$

Where:
- $p \space (Pa)$ is the static pressure.
- $\rho \space (kg/m^3)$ is the fluid density.
- $v \space (m/s)$ is the flow velocity.
- $g \space (m/s^2)$ is acceleration of gravity.
- $h \space (m)$ is the elevation height.
- $E_{\text{shaft}} \space (J/kg)$ is the net shaft energy per unit mass for the turbine.
- $E_{\text{loss}} \space (J/kg)$ is the hydraulic loss through the turbine.

This above equation may not be very usable by us so we can multiply it by $\rho$ to get the equation in terms of energy per unit volume:
$$
p_{\text{in}} + \rho \frac{v_{\text{in}}^2}{2} + \gamma h_{\text{in}} = p_{\text{out}} + \rho \frac{v_{\text{out}}^2}{2} + \gamma h_{\text{out}} + \rho E_{\text{shaft}} + \rho E_{\text{loss}}
$$

Where:
- $\rho E_{\text{shaft}} \space (J/m^3)$ is the net shaft energy per unit mass for the turbine.
- $\rho E_{\text{loss}} \space (J/m^3)$ is the hydraulic loss through the turbine.

The fluid density of air is:
$$
\rho = 1.225 \space kg/m^3
$$

The fluid specific weight of air is:
$$
\gamma = \rho \times g = 1.225 \times 9.81 = 12.01725 \space kg/m^3
$$

Consider the efficiency of the turbine:
$$
\eta = \frac{E_{\text{shaft}}}{E_{\text{shaft}} + E_{\text{loss}}}
$$

The [air duct velocity](https://www.engineeringtoolbox.com/flow-velocity-air-ducts-d_388.html) can vary from $5 - 11 m/s$.

## Aerodynamic Performance

Overall turbine torque:
$$
Q = N\overline{F_{t}}R
$$

Total output power:
$$
P_{\text{out}} = Q\omega
$$

Turbine power coefficient:
$$
CP = \frac{2P_{\text{out}}}{\rho A r U_{\infty}^3}
$$


## Rotor Solidity Factor

## Blade Aspect Ratio

## Rotor Swept Area

## Cut-In Wind Speed

Cut-in wind speed is the lowest wind speed for turbine to generate consistent power.

The turbine needs to generate enough starting torque at this wind speed to overcome its inertia.

> In a worst-case scenario, the motor could draw power from the battery to self-start the turbine.

## Cut-Out Wind Speed

Cut-out wind speed is the highest input wind speed that a turbine should generate consistent power for.

## Turbine Configuration ⚙️

Consider the expected air flow range which is:
$$
v = 3 - 4 \space m/s
$$

Consider the efficiency curves of the turbine configurations:

## Turbine Blade Material Selection


## Generator Selection 🚘

Consider the battery-capacity formula:
$$
E = V \times Q
$$

Where:
- $E \space (Whr)$ is the battery energy.
- $V \space (V)$ is the battery voltage.
- $Q \space (Ahr)$ is the battery capacity.

For two 105075 batteries in series, the total battery energy is:
$$
E_{\text{two in-series}} = 2 \times 4.2 \times 5 = 42 \space Whr
$$

For a single 105075 battery, the battery energy is:
$$
E_{\text{single}} = 4.2 \times 5 = 21 \space Whr
$$

Consider the C-rate relationship with current and battery energy:
$$
I = Cr \times E
$$

Where:
- $I \space (A)$ is the current.
- $E \space (Whr)$ is the battery energy.
- $Cr \space (hr^{-1})$ is the C-rate.

The required current to charge the battery can be calculated:
$$
I_{\text{charge}} = Cr \times E_{\text{single}} = 0.2 \times 21 = 4.2 \space A
$$

To select an appropriate generator for two in-series 105075 batteries, the generator needs to supply at least $8.4 \space V$ and $4.2 \space A$. Therefore, the required generator power is:
$$
P = V \times I = 8.4 \times 4.2 = 35.28 \space W
$$

A table of appropriate motors:
<table>
    <tr>
        <th>Motor</th>
        <th></th>
        <th></th>
    </tr>
</table>

Consider the mechanical generated from the turbine:
$$
P = \tau \times \omega
$$
Where:
- $\tau \space (Nm)$ is the torque of the turbine.
- $\omega \space (ms^{-1})$ is the rotational speed of the turbine.

> System design calculations were made in this [Google Sheet](https://docs.google.com/spreadsheets/d/1eosVVQOt2COTTdD-d0bvh6w1MXfZiy1iHKO29cC1Ua0/edit?usp=sharing).

## Bearing Selection 🛞

The expected rotational speed of the turbine is thus:

## Circlip Selection

## Bolt Selection

## Verification

## Validation