# Prototype 🧱

Building a proof-of-concept.

## Work Packages 💼

[TOC]

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
.tg .tg-clww{background-color:#F6D568;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-06ha{background-color:#EB8F71;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-4ivf{background-color:#E78273;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-090p{background-color:#C1CC73;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-vr9z{background-color:#E67F73;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-d6lg{background-color:#E98872;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-3io6{background-color:#6BBF85;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-4vur{background-color:#E98972;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-vg9x{background-color:#E8D36B;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-vwkk{background-color:#FBD667;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-kegi{background-color:#F4D568;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-jsqk{background-color:#91C57D;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-mf1y{background-color:#97C67C;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-zj55{background-color:#A4C879;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-em69{background-color:#FFD666;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-7btt{border-color:inherit;font-weight:bold;text-align:center;vertical-align:top}
.tg .tg-fll5{border-color:inherit;font-weight:bold;text-align:center;vertical-align:bottom}
.tg .tg-fchy{background-color:#E67C73;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-u0wo{background-color:#E88572;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-plpd{background-color:#ED9570;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-dfxj{background-color:#EE9C6F;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-7vq7{background-color:#F2A96D;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-f5cs{background-color:#F6B56B;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-n0he{background-color:#F9C269;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-nn8n{background-color:#E67D73;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-n6dw{background-color:#E78173;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-fbrj{background-color:#EA8D71;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-pmy1{background-color:#EF9D6F;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-6shm{background-color:#F1A56D;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-30wt{background-color:#FAC569;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-lq5z{background-color:#E88472;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-wt7h{background-color:#EC9270;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-pd65{background-color:#F4AF6C;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-ljj2{background-color:#FED666;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-x1n4{background-color:#F7D567;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-twob{background-color:#F1D469;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-q0ei{background-color:#F0D469;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-qgp5{background-color:#DED16D;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-kpva{background-color:#E4D26B;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-1yt7{background-color:#D7D06E;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-dzpk{background-color:#CBCE71;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-f2ym{background-color:#C8CE71;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-6qrj{background-color:#B7CB75;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-88pj{background-color:#F0A26E;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-ccbk{background-color:#F6B96B;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-rcvj{background-color:#FDCF67;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-dqzg{background-color:#FCD666;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-97r8{background-color:#EBD36A;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-0495{background-color:#DFD16C;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-okop{background-color:#D4D06F;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-v8nh{background-color:#BECC74;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-lt8a{background-color:#A8C878;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-9d2x{background-color:#B1CA76;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-b1z7{background-color:#7EC281;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-st3g{background-color:#FCCC68;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-d411{background-color:#ECD36A;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-ylbp{background-color:#D0CF70;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-ewaz{background-color:#87C37F;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-kp2v{background-color:#78C183;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-j1aw{background-color:#57BB8A;border-color:inherit;text-align:center;vertical-align:bottom}
</style>
<table class="tg">
<thead>
  <tr>
    <th class="tg-7btt" rowspan="2">Width (mm)</th>
    <th class="tg-fll5" colspan="11"><span style="font-weight:bold">Height (mm)</span></th>
  </tr>
  <tr>
    <th class="tg-fll5"><span style="font-weight:bold">100</span></th>
    <th class="tg-fll5"><span style="font-weight:bold">150</span></th>
    <th class="tg-fll5"><span style="font-weight:bold">200</span></th>
    <th class="tg-fll5"><span style="font-weight:bold">250</span></th>
    <th class="tg-fll5"><span style="font-weight:bold">300</span></th>
    <th class="tg-fll5"><span style="font-weight:bold">400</span></th>
    <th class="tg-fll5"><span style="font-weight:bold">500</span></th>
    <th class="tg-fll5"><span style="font-weight:bold">600</span></th>
    <th class="tg-fll5"><span style="font-weight:bold">800</span></th>
    <th class="tg-fll5"><span style="font-weight:bold">1000</span></th>
    <th class="tg-fll5"><span style="font-weight:bold">1200</span></th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">200</span></td>
    <td class="tg-fchy"><span style="font-weight:normal;background-color:#E67C73">1.53</span></td>
    <td class="tg-vr9z">2.30</td>
    <td class="tg-4ivf"><span style="font-weight:normal;background-color:#E78273">3.06</span></td>
    <td class="tg-u0wo">3.83</td>
    <td class="tg-d6lg">4.59</td>
    <td class="tg-06ha">6.13</td>
    <td class="tg-plpd">7.66</td>
    <td class="tg-dfxj">9.19</td>
    <td class="tg-7vq7">12.25</td>
    <td class="tg-f5cs">15.31</td>
    <td class="tg-n0he">18.38</td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">250</span></td>
    <td class="tg-nn8n"><span style="font-weight:normal;background-color:#E67D73">1.91</span></td>
    <td class="tg-n6dw"><span style="font-weight:normal;background-color:#E78173">2.87</span></td>
    <td class="tg-u0wo">3.83</td>
    <td class="tg-4vur">4.79</td>
    <td class="tg-fbrj">5.74</td>
    <td class="tg-plpd">7.66</td>
    <td class="tg-pmy1">9.57</td>
    <td class="tg-6shm">11.48</td>
    <td class="tg-f5cs">15.31</td>
    <td class="tg-30wt">19.14</td>
    <td class="tg-em69"><span style="font-weight:normal;background-color:#FFD666">22.97</span></td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">300</span></td>
    <td class="tg-vr9z">2.30</td>
    <td class="tg-lq5z">3.45</td>
    <td class="tg-d6lg">4.59</td>
    <td class="tg-fbrj">5.74</td>
    <td class="tg-wt7h">6.89</td>
    <td class="tg-dfxj">9.19</td>
    <td class="tg-6shm">11.48</td>
    <td class="tg-pd65">13.78</td>
    <td class="tg-n0he">18.38</td>
    <td class="tg-em69"><span style="font-weight:normal;background-color:#FFD666">22.97</span></td>
    <td class="tg-vwkk">27.56</td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">400</span></td>
    <td class="tg-4ivf"><span style="font-weight:normal;background-color:#E78273">3.06</span></td>
    <td class="tg-d6lg">4.59</td>
    <td class="tg-06ha">6.13</td>
    <td class="tg-plpd">7.66</td>
    <td class="tg-dfxj">9.19</td>
    <td class="tg-7vq7">12.25</td>
    <td class="tg-f5cs">15.31</td>
    <td class="tg-n0he">18.38</td>
    <td class="tg-ljj2"><span style="font-weight:normal;background-color:#FED666">24.50</span></td>
    <td class="tg-x1n4"><span style="font-weight:normal;background-color:#F7D567">30.63</span></td>
    <td class="tg-twob">36.75</td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">500</span></td>
    <td class="tg-u0wo">3.83</td>
    <td class="tg-fbrj">5.74</td>
    <td class="tg-plpd">7.66</td>
    <td class="tg-pmy1">9.57</td>
    <td class="tg-6shm">11.48</td>
    <td class="tg-f5cs">15.31</td>
    <td class="tg-30wt">19.14</td>
    <td class="tg-em69"><span style="font-weight:normal;background-color:#FFD666">22.97</span></td>
    <td class="tg-x1n4"><span style="font-weight:normal;background-color:#F7D567">30.63</span></td>
    <td class="tg-q0ei"><span style="font-weight:normal;background-color:#F0D469">38.28</span></td>
    <td class="tg-vg9x">45.94</td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">600</span></td>
    <td class="tg-d6lg">4.59</td>
    <td class="tg-wt7h">6.89</td>
    <td class="tg-dfxj">9.19</td>
    <td class="tg-6shm">11.48</td>
    <td class="tg-pd65">13.78</td>
    <td class="tg-n0he">18.38</td>
    <td class="tg-em69"><span style="font-weight:normal;background-color:#FFD666">22.97</span></td>
    <td class="tg-vwkk">27.56</td>
    <td class="tg-twob">36.75</td>
    <td class="tg-vg9x">45.94</td>
    <td class="tg-qgp5">55.13</td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">800</span></td>
    <td class="tg-06ha">6.13</td>
    <td class="tg-dfxj">9.19</td>
    <td class="tg-7vq7">12.25</td>
    <td class="tg-f5cs">15.31</td>
    <td class="tg-n0he">18.38</td>
    <td class="tg-ljj2"><span style="font-weight:normal;background-color:#FED666">24.50</span></td>
    <td class="tg-x1n4"><span style="font-weight:normal;background-color:#F7D567">30.63</span></td>
    <td class="tg-twob">36.75</td>
    <td class="tg-kpva"><span style="font-weight:normal;background-color:#E4D26B">49.00</span></td>
    <td class="tg-1yt7">61.25</td>
    <td class="tg-dzpk">73.50</td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">1000</span></td>
    <td class="tg-plpd">7.66</td>
    <td class="tg-6shm">11.48</td>
    <td class="tg-f5cs">15.31</td>
    <td class="tg-30wt">19.14</td>
    <td class="tg-em69"><span style="font-weight:normal;background-color:#FFD666">22.97</span></td>
    <td class="tg-x1n4"><span style="font-weight:normal;background-color:#F7D567">30.63</span></td>
    <td class="tg-q0ei"><span style="font-weight:normal;background-color:#F0D469">38.28</span></td>
    <td class="tg-vg9x">45.94</td>
    <td class="tg-1yt7">61.25</td>
    <td class="tg-f2ym">76.56</td>
    <td class="tg-6qrj">91.88</td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">1200</span></td>
    <td class="tg-dfxj">9.19</td>
    <td class="tg-pd65">13.78</td>
    <td class="tg-n0he">18.38</td>
    <td class="tg-em69"><span style="font-weight:normal;background-color:#FFD666">22.97</span></td>
    <td class="tg-vwkk">27.56</td>
    <td class="tg-twob">36.75</td>
    <td class="tg-vg9x">45.94</td>
    <td class="tg-qgp5">55.13</td>
    <td class="tg-dzpk">73.50</td>
    <td class="tg-6qrj">91.88</td>
    <td class="tg-zj55">110.25</td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">1400</span></td>
    <td class="tg-88pj">10.72</td>
    <td class="tg-ccbk">16.08</td>
    <td class="tg-rcvj">21.44</td>
    <td class="tg-dqzg">26.80</td>
    <td class="tg-clww">32.16</td>
    <td class="tg-97r8"><span style="font-weight:normal;background-color:#EBD36A">42.88</span></td>
    <td class="tg-0495">53.59</td>
    <td class="tg-okop">64.31</td>
    <td class="tg-v8nh"><span style="font-weight:normal;background-color:#BECC74">85.75</span></td>
    <td class="tg-lt8a">107.19</td>
    <td class="tg-jsqk">128.63</td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">1600</span></td>
    <td class="tg-7vq7">12.25</td>
    <td class="tg-n0he">18.38</td>
    <td class="tg-ljj2"><span style="font-weight:normal;background-color:#FED666">24.50</span></td>
    <td class="tg-x1n4"><span style="font-weight:normal;background-color:#F7D567">30.63</span></td>
    <td class="tg-twob">36.75</td>
    <td class="tg-kpva"><span style="font-weight:normal;background-color:#E4D26B">49.00</span></td>
    <td class="tg-1yt7">61.25</td>
    <td class="tg-dzpk">73.50</td>
    <td class="tg-9d2x">98.00</td>
    <td class="tg-mf1y">122.50</td>
    <td class="tg-b1z7">147.00</td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">1800</span></td>
    <td class="tg-pd65">13.78</td>
    <td class="tg-st3g">20.67</td>
    <td class="tg-vwkk">27.56</td>
    <td class="tg-kegi">34.45</td>
    <td class="tg-d411">41.34</td>
    <td class="tg-qgp5">55.13</td>
    <td class="tg-ylbp"><span style="font-weight:normal;background-color:#D0CF70">68.91</span></td>
    <td class="tg-090p">82.69</td>
    <td class="tg-zj55">110.25</td>
    <td class="tg-ewaz">137.81</td>
    <td class="tg-3io6">165.38</td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">2000</span></td>
    <td class="tg-f5cs">15.31</td>
    <td class="tg-em69"><span style="font-weight:normal;background-color:#FFD666">22.97</span></td>
    <td class="tg-x1n4"><span style="font-weight:normal;background-color:#F7D567">30.63</span></td>
    <td class="tg-q0ei"><span style="font-weight:normal;background-color:#F0D469">38.28</span></td>
    <td class="tg-vg9x">45.94</td>
    <td class="tg-1yt7">61.25</td>
    <td class="tg-f2ym">76.56</td>
    <td class="tg-6qrj">91.88</td>
    <td class="tg-mf1y">122.50</td>
    <td class="tg-kp2v">153.13</td>
    <td class="tg-j1aw">183.75</td>
  </tr>
</tbody>
</table>

To get the maximum effective turbine power, the maximum extractable fluid power is multiplied by [Betz's coefficient](https://en.wikipedia.org/wiki/Betz%27s_law):
$$
P_{\text{turbine}} = \frac{16}{27} \times P_{\text{fluid}}
$$

The following table shows the maximum effective turbine power vs air duct sizes:

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  overflow:hidden;padding:10px 5px;word-break:normal;}
.tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  font-weight:normal;overflow:hidden;padding:10px 5px;word-break:normal;}
.tg .tg-23jy{background-color:#ED9670;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-420o{background-color:#E67E73;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-lhc5{background-color:#E98772;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-xocn{background-color:#E88672;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-4ivf{background-color:#E78273;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-dfko{background-color:#DDD16D;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-1xgm{background-color:#D6D06E;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-2vc3{background-color:#C7CD72;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-gi6p{background-color:#F5D568;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-502n{background-color:#EFD469;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-styj{background-color:#E2D26C;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-f3sz{background-color:#B5CA76;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-wlh0{background-color:#F3D468;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-z7se{background-color:#F9D567;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-zcjq{background-color:#E7D36B;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-zsud{background-color:#FAD667;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-zlag{background-color:#F9C06A;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-em69{background-color:#FFD666;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-7btt{border-color:inherit;font-weight:bold;text-align:center;vertical-align:top}
.tg .tg-fll5{border-color:inherit;font-weight:bold;text-align:center;vertical-align:bottom}
.tg .tg-fchy{background-color:#E67C73;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-n6dw{background-color:#E78173;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-dffa{background-color:#E88372;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-yqa5{background-color:#EA8B71;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-km6z{background-color:#EB9170;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-zxyu{background-color:#F0A16E;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-iind{background-color:#F3AB6D;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-ng3h{background-color:#F6B66B;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-nn8n{background-color:#E67D73;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-evn7{background-color:#E78073;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-qfjg{background-color:#EA8A71;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-dwsa{background-color:#ED976F;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-xxoq{background-color:#EF9E6F;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-41kv{background-color:#F6B86B;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-bbni{background-color:#FAC669;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-ris1{background-color:#EB8E71;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-f38b{background-color:#F1A66D;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-kicr{background-color:#FCCB68;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-ljj2{background-color:#FED666;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-97r8{background-color:#EBD36A;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-kpva{background-color:#E4D26B;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-9rct{background-color:#D9D06E;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-zokr{background-color:#CECF70;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-556u{background-color:#EE9B6F;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-d65n{background-color:#F3AE6C;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-qw0s{background-color:#FED367;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-hn99{background-color:#FDD666;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-t5db{background-color:#F6D567;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-q0ei{background-color:#F0D469;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-5bhf{background-color:#EAD36A;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-ylbp{background-color:#D0CF70;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-lljt{background-color:#C3CD72;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-an1c{background-color:#B8CB75;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-lj0t{background-color:#F8BE6A;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-9upn{background-color:#FBD666;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-x1n4{background-color:#F7D567;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-ucyy{background-color:#DFD16D;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-v8nh{background-color:#BECC74;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-6euf{background-color:#AEC977;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-0mk6{background-color:#A3C879;border-color:inherit;text-align:center;vertical-align:bottom}
</style>
<table class="tg">
<thead>
  <tr>
    <th class="tg-7btt" rowspan="2">Width (mm)</th>
    <th class="tg-fll5" colspan="11"><span style="font-weight:bold">Height (mm)</span></th>
  </tr>
  <tr>
    <th class="tg-fll5"><span style="font-weight:bold">100</span></th>
    <th class="tg-fll5"><span style="font-weight:bold">150</span></th>
    <th class="tg-fll5"><span style="font-weight:bold">200</span></th>
    <th class="tg-fll5"><span style="font-weight:bold">250</span></th>
    <th class="tg-fll5"><span style="font-weight:bold">300</span></th>
    <th class="tg-fll5"><span style="font-weight:bold">400</span></th>
    <th class="tg-fll5"><span style="font-weight:bold">500</span></th>
    <th class="tg-fll5"><span style="font-weight:bold">600</span></th>
    <th class="tg-fll5"><span style="font-weight:bold">800</span></th>
    <th class="tg-fll5"><span style="font-weight:bold">1000</span></th>
    <th class="tg-fll5"><span style="font-weight:bold">1200</span></th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">200</span></td>
    <td class="tg-fchy"><span style="font-weight:normal;background-color:#E67C73">0.91</span></td>
    <td class="tg-420o"><span style="font-weight:normal;background-color:#E67E73">1.36</span></td>
    <td class="tg-n6dw"><span style="font-weight:normal;background-color:#E78173">1.81</span></td>
    <td class="tg-dffa"><span style="font-weight:normal;background-color:#E88372">2.27</span></td>
    <td class="tg-xocn"><span style="font-weight:normal;background-color:#E88672">2.72</span></td>
    <td class="tg-yqa5"><span style="font-weight:normal;background-color:#EA8B71">3.63</span></td>
    <td class="tg-km6z"><span style="font-weight:normal;background-color:#EB9170">4.54</span></td>
    <td class="tg-23jy"><span style="font-weight:normal;background-color:#ED9670">5.44</span></td>
    <td class="tg-zxyu"><span style="font-weight:normal;background-color:#F0A16E">7.26</span></td>
    <td class="tg-iind"><span style="font-weight:normal;background-color:#F3AB6D">9.07</span></td>
    <td class="tg-ng3h"><span style="font-weight:normal;background-color:#F6B66B">10.89</span></td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">250</span></td>
    <td class="tg-nn8n"><span style="font-weight:normal;background-color:#E67D73">1.13</span></td>
    <td class="tg-evn7"><span style="font-weight:normal;background-color:#E78073">1.70</span></td>
    <td class="tg-dffa"><span style="font-weight:normal;background-color:#E88372">2.27</span></td>
    <td class="tg-lhc5"><span style="font-weight:normal;background-color:#E98772">2.84</span></td>
    <td class="tg-qfjg"><span style="font-weight:normal;background-color:#EA8A71">3.40</span></td>
    <td class="tg-km6z"><span style="font-weight:normal;background-color:#EB9170">4.54</span></td>
    <td class="tg-dwsa"><span style="font-weight:normal;background-color:#ED976F">5.67</span></td>
    <td class="tg-xxoq"><span style="font-weight:normal;background-color:#EF9E6F">6.81</span></td>
    <td class="tg-iind"><span style="font-weight:normal;background-color:#F3AB6D">9.07</span></td>
    <td class="tg-41kv"><span style="font-weight:normal;background-color:#F6B86B">11.34</span></td>
    <td class="tg-bbni"><span style="font-weight:normal;background-color:#FAC669">13.61</span></td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">300</span></td>
    <td class="tg-420o"><span style="font-weight:normal;background-color:#E67E73">1.36</span></td>
    <td class="tg-4ivf"><span style="font-weight:normal;background-color:#E78273">2.04</span></td>
    <td class="tg-xocn"><span style="font-weight:normal;background-color:#E88672">2.72</span></td>
    <td class="tg-qfjg"><span style="font-weight:normal;background-color:#EA8A71">3.40</span></td>
    <td class="tg-ris1"><span style="font-weight:normal;background-color:#EB8E71">4.08</span></td>
    <td class="tg-23jy"><span style="font-weight:normal;background-color:#ED9670">5.44</span></td>
    <td class="tg-xxoq"><span style="font-weight:normal;background-color:#EF9E6F">6.81</span></td>
    <td class="tg-f38b"><span style="font-weight:normal;background-color:#F1A66D">8.17</span></td>
    <td class="tg-ng3h"><span style="font-weight:normal;background-color:#F6B66B">10.89</span></td>
    <td class="tg-bbni"><span style="font-weight:normal;background-color:#FAC669">13.61</span></td>
    <td class="tg-em69"><span style="font-weight:normal;background-color:#FFD666">16.33</span></td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">400</span></td>
    <td class="tg-n6dw"><span style="font-weight:normal;background-color:#E78173">1.81</span></td>
    <td class="tg-xocn"><span style="font-weight:normal;background-color:#E88672">2.72</span></td>
    <td class="tg-yqa5"><span style="font-weight:normal;background-color:#EA8B71">3.63</span></td>
    <td class="tg-km6z"><span style="font-weight:normal;background-color:#EB9170">4.54</span></td>
    <td class="tg-23jy"><span style="font-weight:normal;background-color:#ED9670">5.44</span></td>
    <td class="tg-zxyu"><span style="font-weight:normal;background-color:#F0A16E">7.26</span></td>
    <td class="tg-iind"><span style="font-weight:normal;background-color:#F3AB6D">9.07</span></td>
    <td class="tg-ng3h"><span style="font-weight:normal;background-color:#F6B66B">10.89</span></td>
    <td class="tg-kicr"><span style="font-weight:normal;background-color:#FCCB68">14.52</span></td>
    <td class="tg-ljj2"><span style="font-weight:normal;background-color:#FED666">18.15</span></td>
    <td class="tg-zsud"><span style="font-weight:normal;background-color:#FAD667">21.78</span></td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">500</span></td>
    <td class="tg-dffa"><span style="font-weight:normal;background-color:#E88372">2.27</span></td>
    <td class="tg-qfjg"><span style="font-weight:normal;background-color:#EA8A71">3.40</span></td>
    <td class="tg-km6z"><span style="font-weight:normal;background-color:#EB9170">4.54</span></td>
    <td class="tg-dwsa"><span style="font-weight:normal;background-color:#ED976F">5.67</span></td>
    <td class="tg-xxoq"><span style="font-weight:normal;background-color:#EF9E6F">6.81</span></td>
    <td class="tg-iind"><span style="font-weight:normal;background-color:#F3AB6D">9.07</span></td>
    <td class="tg-41kv"><span style="font-weight:normal;background-color:#F6B86B">11.34</span></td>
    <td class="tg-bbni"><span style="font-weight:normal;background-color:#FAC669">13.61</span></td>
    <td class="tg-ljj2"><span style="font-weight:normal;background-color:#FED666">18.15</span></td>
    <td class="tg-z7se"><span style="font-weight:normal;background-color:#F9D567">22.69</span></td>
    <td class="tg-gi6p"><span style="font-weight:normal;background-color:#F5D568">27.22</span></td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">600</span></td>
    <td class="tg-xocn"><span style="font-weight:normal;background-color:#E88672">2.72</span></td>
    <td class="tg-ris1"><span style="font-weight:normal;background-color:#EB8E71">4.08</span></td>
    <td class="tg-23jy"><span style="font-weight:normal;background-color:#ED9670">5.44</span></td>
    <td class="tg-xxoq"><span style="font-weight:normal;background-color:#EF9E6F">6.81</span></td>
    <td class="tg-f38b"><span style="font-weight:normal;background-color:#F1A66D">8.17</span></td>
    <td class="tg-ng3h"><span style="font-weight:normal;background-color:#F6B66B">10.89</span></td>
    <td class="tg-bbni"><span style="font-weight:normal;background-color:#FAC669">13.61</span></td>
    <td class="tg-em69"><span style="font-weight:normal;background-color:#FFD666">16.33</span></td>
    <td class="tg-zsud"><span style="font-weight:normal;background-color:#FAD667">21.78</span></td>
    <td class="tg-gi6p"><span style="font-weight:normal;background-color:#F5D568">27.22</span></td>
    <td class="tg-502n"><span style="font-weight:normal;background-color:#EFD469">32.67</span></td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">800</span></td>
    <td class="tg-yqa5"><span style="font-weight:normal;background-color:#EA8B71">3.63</span></td>
    <td class="tg-23jy"><span style="font-weight:normal;background-color:#ED9670">5.44</span></td>
    <td class="tg-zxyu"><span style="font-weight:normal;background-color:#F0A16E">7.26</span></td>
    <td class="tg-iind"><span style="font-weight:normal;background-color:#F3AB6D">9.07</span></td>
    <td class="tg-ng3h"><span style="font-weight:normal;background-color:#F6B66B">10.89</span></td>
    <td class="tg-kicr"><span style="font-weight:normal;background-color:#FCCB68">14.52</span></td>
    <td class="tg-ljj2"><span style="font-weight:normal;background-color:#FED666">18.15</span></td>
    <td class="tg-zsud"><span style="font-weight:normal;background-color:#FAD667">21.78</span></td>
    <td class="tg-wlh0"><span style="font-weight:normal;background-color:#F3D468">29.04</span></td>
    <td class="tg-97r8"><span style="font-weight:normal;background-color:#EBD36A">36.30</span></td>
    <td class="tg-kpva"><span style="font-weight:normal;background-color:#E4D26B">43.56</span></td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">1000</span></td>
    <td class="tg-km6z"><span style="font-weight:normal;background-color:#EB9170">4.54</span></td>
    <td class="tg-xxoq"><span style="font-weight:normal;background-color:#EF9E6F">6.81</span></td>
    <td class="tg-iind"><span style="font-weight:normal;background-color:#F3AB6D">9.07</span></td>
    <td class="tg-41kv"><span style="font-weight:normal;background-color:#F6B86B">11.34</span></td>
    <td class="tg-bbni"><span style="font-weight:normal;background-color:#FAC669">13.61</span></td>
    <td class="tg-ljj2"><span style="font-weight:normal;background-color:#FED666">18.15</span></td>
    <td class="tg-z7se"><span style="font-weight:normal;background-color:#F9D567">22.69</span></td>
    <td class="tg-gi6p"><span style="font-weight:normal;background-color:#F5D568">27.22</span></td>
    <td class="tg-97r8"><span style="font-weight:normal;background-color:#EBD36A">36.30</span></td>
    <td class="tg-styj"><span style="font-weight:normal;background-color:#E2D26C">45.37</span></td>
    <td class="tg-9rct"><span style="font-weight:normal;background-color:#D9D06E">54.44</span></td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">1200</span></td>
    <td class="tg-23jy"><span style="font-weight:normal;background-color:#ED9670">5.44</span></td>
    <td class="tg-f38b"><span style="font-weight:normal;background-color:#F1A66D">8.17</span></td>
    <td class="tg-ng3h"><span style="font-weight:normal;background-color:#F6B66B">10.89</span></td>
    <td class="tg-bbni"><span style="font-weight:normal;background-color:#FAC669">13.61</span></td>
    <td class="tg-em69"><span style="font-weight:normal;background-color:#FFD666">16.33</span></td>
    <td class="tg-zsud"><span style="font-weight:normal;background-color:#FAD667">21.78</span></td>
    <td class="tg-gi6p"><span style="font-weight:normal;background-color:#F5D568">27.22</span></td>
    <td class="tg-502n"><span style="font-weight:normal;background-color:#EFD469">32.67</span></td>
    <td class="tg-kpva"><span style="font-weight:normal;background-color:#E4D26B">43.56</span></td>
    <td class="tg-9rct"><span style="font-weight:normal;background-color:#D9D06E">54.44</span></td>
    <td class="tg-zokr"><span style="font-weight:normal;background-color:#CECF70">65.33</span></td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">1400</span></td>
    <td class="tg-556u"><span style="font-weight:normal;background-color:#EE9B6F">6.35</span></td>
    <td class="tg-d65n"><span style="font-weight:normal;background-color:#F3AE6C">9.53</span></td>
    <td class="tg-zlag"><span style="font-weight:normal;background-color:#F9C06A">12.70</span></td>
    <td class="tg-qw0s"><span style="font-weight:normal;background-color:#FED367">15.88</span></td>
    <td class="tg-hn99"><span style="font-weight:normal;background-color:#FDD666">19.06</span></td>
    <td class="tg-t5db"><span style="font-weight:normal;background-color:#F6D567">25.41</span></td>
    <td class="tg-q0ei"><span style="font-weight:normal;background-color:#F0D469">31.76</span></td>
    <td class="tg-5bhf"><span style="font-weight:normal;background-color:#EAD36A">38.11</span></td>
    <td class="tg-dfko"><span style="font-weight:normal;background-color:#DDD16D">50.81</span></td>
    <td class="tg-ylbp"><span style="font-weight:normal;background-color:#D0CF70">63.52</span></td>
    <td class="tg-lljt"><span style="font-weight:normal;background-color:#C3CD72">76.22</span></td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">1600</span></td>
    <td class="tg-zxyu"><span style="font-weight:normal;background-color:#F0A16E">7.26</span></td>
    <td class="tg-ng3h"><span style="font-weight:normal;background-color:#F6B66B">10.89</span></td>
    <td class="tg-kicr"><span style="font-weight:normal;background-color:#FCCB68">14.52</span></td>
    <td class="tg-ljj2"><span style="font-weight:normal;background-color:#FED666">18.15</span></td>
    <td class="tg-zsud"><span style="font-weight:normal;background-color:#FAD667">21.78</span></td>
    <td class="tg-wlh0"><span style="font-weight:normal;background-color:#F3D468">29.04</span></td>
    <td class="tg-97r8"><span style="font-weight:normal;background-color:#EBD36A">36.30</span></td>
    <td class="tg-kpva"><span style="font-weight:normal;background-color:#E4D26B">43.56</span></td>
    <td class="tg-1xgm"><span style="font-weight:normal;background-color:#D6D06E">58.07</span></td>
    <td class="tg-2vc3"><span style="font-weight:normal;background-color:#C7CD72">72.59</span></td>
    <td class="tg-an1c"><span style="font-weight:normal;background-color:#B8CB75">87.11</span></td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">1800</span></td>
    <td class="tg-f38b"><span style="font-weight:normal;background-color:#F1A66D">8.17</span></td>
    <td class="tg-lj0t"><span style="font-weight:normal;background-color:#F8BE6A">12.25</span></td>
    <td class="tg-em69"><span style="font-weight:normal;background-color:#FFD666">16.33</span></td>
    <td class="tg-9upn"><span style="font-weight:normal;background-color:#FBD666">20.42</span></td>
    <td class="tg-x1n4"><span style="font-weight:normal;background-color:#F7D567">24.50</span></td>
    <td class="tg-502n"><span style="font-weight:normal;background-color:#EFD469">32.67</span></td>
    <td class="tg-zcjq"><span style="font-weight:normal;background-color:#E7D36B">40.83</span></td>
    <td class="tg-ucyy"><span style="font-weight:normal;background-color:#DFD16D">49.00</span></td>
    <td class="tg-zokr"><span style="font-weight:normal;background-color:#CECF70">65.33</span></td>
    <td class="tg-v8nh"><span style="font-weight:normal;background-color:#BECC74">81.67</span></td>
    <td class="tg-6euf"><span style="font-weight:normal;background-color:#AEC977">98.00</span></td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">2000</span></td>
    <td class="tg-iind"><span style="font-weight:normal;background-color:#F3AB6D">9.07</span></td>
    <td class="tg-bbni"><span style="font-weight:normal;background-color:#FAC669">13.61</span></td>
    <td class="tg-ljj2"><span style="font-weight:normal;background-color:#FED666">18.15</span></td>
    <td class="tg-z7se"><span style="font-weight:normal;background-color:#F9D567">22.69</span></td>
    <td class="tg-gi6p"><span style="font-weight:normal;background-color:#F5D568">27.22</span></td>
    <td class="tg-97r8"><span style="font-weight:normal;background-color:#EBD36A">36.30</span></td>
    <td class="tg-styj"><span style="font-weight:normal;background-color:#E2D26C">45.37</span></td>
    <td class="tg-9rct"><span style="font-weight:normal;background-color:#D9D06E">54.44</span></td>
    <td class="tg-2vc3"><span style="font-weight:normal;background-color:#C7CD72">72.59</span></td>
    <td class="tg-f3sz"><span style="font-weight:normal;background-color:#B5CA76">90.74</span></td>
    <td class="tg-0mk6"><span style="font-weight:normal;background-color:#A3C879">108.89</span></td>
  </tr>
</tbody>
</table>

> [Betz's Law](https://en.wikipedia.org/wiki/Betz%27s_law) states that no turbine can capture more than 59.3% of the kinetic energy of the wind.

## Sensor Array Selection ⚡️

> Research on sensors in this [Google Sheet](https://docs.google.com/spreadsheets/d/1f3vsNErERXZ-9NdXlSl-dcCkEAP_58Zadz2kLJG4f4g/edit#gid=0).

## Mechatronic System Power Requirements 🤖

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

An efficient mechatronic system would only allow a single sensor device to be enabled at a time (with the microcontroller and wifi module enabled as well). Power use can be summed from considering the voltage and current ratings of the devices:
$$
\begin{aligned}
P_{\text{mechatronic system}} &= P_{\text{Arduino Nano}} + P_{\text{USB-C}} + P_{\text{TinyPICO}} \\
&= 7 \times 0.02 + 5 \times 1.5 + 2 \times 0.09 \\
&= 7.82 \space W
\end{aligned}
$$

Compare this power requirement to the table of maximum effective turbine powers (red cells are nonviable to power a turbine, green cells are viable):

<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  overflow:hidden;padding:10px 5px;word-break:normal;}
.tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  font-weight:normal;overflow:hidden;padding:10px 5px;word-break:normal;}
.tg .tg-y9p2{background-color:#EA4335;border-color:inherit;text-align:center;vertical-align:bottom}
.tg .tg-7btt{border-color:inherit;font-weight:bold;text-align:center;vertical-align:top}
.tg .tg-fll5{border-color:inherit;font-weight:bold;text-align:center;vertical-align:bottom}
.tg .tg-kd2b{background-color:#34A853;border-color:inherit;text-align:center;vertical-align:bottom}
</style>
<table class="tg">
<thead>
  <tr>
    <th class="tg-7btt" rowspan="2">Width (mm)</th>
    <th class="tg-fll5" colspan="11"><span style="font-weight:bold">Height (mm)</span></th>
  </tr>
  <tr>
    <th class="tg-fll5"><span style="font-weight:bold">100</span></th>
    <th class="tg-fll5"><span style="font-weight:bold">150</span></th>
    <th class="tg-fll5"><span style="font-weight:bold">200</span></th>
    <th class="tg-fll5"><span style="font-weight:bold">250</span></th>
    <th class="tg-fll5"><span style="font-weight:bold">300</span></th>
    <th class="tg-fll5"><span style="font-weight:bold">400</span></th>
    <th class="tg-fll5"><span style="font-weight:bold">500</span></th>
    <th class="tg-fll5"><span style="font-weight:bold">600</span></th>
    <th class="tg-fll5"><span style="font-weight:bold">800</span></th>
    <th class="tg-fll5"><span style="font-weight:bold">1000</span></th>
    <th class="tg-fll5"><span style="font-weight:bold">1200</span></th>
  </tr>
</thead>
<tbody>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">200</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">0.91</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">1.36</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">1.81</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">2.27</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">2.72</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">3.63</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">4.54</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">5.44</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">7.26</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">9.07</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">10.89</span></td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">250</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">1.13</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">1.70</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">2.27</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">2.84</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">3.40</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">4.54</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">5.67</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">6.81</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">9.07</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">11.34</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">13.61</span></td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">300</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">1.36</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">2.04</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">2.72</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">3.40</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">4.08</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">5.44</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">6.81</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">8.17</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">10.89</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">13.61</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">16.33</span></td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">400</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">1.81</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">2.72</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">3.63</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">4.54</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">5.44</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">7.26</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">9.07</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">10.89</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">14.52</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">18.15</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">21.78</span></td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">500</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">2.27</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">3.40</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">4.54</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">5.67</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">6.81</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">9.07</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">11.34</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">13.61</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">18.15</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">22.69</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">27.22</span></td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">600</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">2.72</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">4.08</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">5.44</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">6.81</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">8.17</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">10.89</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">13.61</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">16.33</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">21.78</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">27.22</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">32.67</span></td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">800</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">3.63</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">5.44</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">7.26</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">9.07</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">10.89</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">14.52</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">18.15</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">21.78</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">29.04</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">36.30</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">43.56</span></td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">1000</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">4.54</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">6.81</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">9.07</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">11.34</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">13.61</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">18.15</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">22.69</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">27.22</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">36.30</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">45.37</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">54.44</span></td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">1200</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">5.44</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">8.17</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">10.89</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">13.61</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">16.33</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">21.78</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">27.22</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">32.67</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">43.56</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">54.44</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">65.33</span></td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">1400</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">6.35</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">9.53</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">12.70</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">15.88</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">19.06</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">25.41</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">31.76</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">38.11</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">50.81</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">63.52</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">76.22</span></td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">1600</span></td>
    <td class="tg-y9p2"><span style="font-weight:normal;background-color:#EA4335">7.26</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">10.89</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">14.52</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">18.15</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">21.78</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">29.04</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">36.30</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">43.56</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">58.07</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">72.59</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">87.11</span></td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">1800</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">8.17</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">12.25</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">16.33</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">20.42</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">24.50</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">32.67</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">40.83</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">49.00</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">65.33</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">81.67</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">98.00</span></td>
  </tr>
  <tr>
    <td class="tg-fll5"><span style="font-weight:bold">2000</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">9.07</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">13.61</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">18.15</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">22.69</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">27.22</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">36.30</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">45.37</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">54.44</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">72.59</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">90.74</span></td>
    <td class="tg-kd2b"><span style="font-weight:normal;background-color:#34A853">108.89</span></td>
  </tr>
</tbody>
</table>

## Battery Selection 🔋

The mechatronic system will draw a current at most:
$$
\begin{aligned}
I_{\text{effective}} = 20 + 1500 + 90 = 1610 \space mA \approx 1.61 \space A
\end{aligned}
$$

When the system is at "rest", the current load would realistically be the current draw of the microcontroller:
$$
I_{\text{rest}} = 20 \space mA = 0.02 \space A
$$

> The current draw of a wifi module at rest is $20 \space \mu A$. The sensors may be turned off when not in use.

### Discharge Current Constraint

The effective discharge current should not be more than $1/10$ of the rated capacity:
$$
\begin{aligned}
I_{\text{effective}} &= \frac{1}{10} \times Q \\
1.61 &= \frac{1}{10} \times Q \\
\therefore Q &= 16.1 \space A \\
\end{aligned}
$$

### Effective Battery Capacity

The battery's effective capacity is $2/3$ of its rated capacity:
$$
\begin{aligned}
Q_{\text{effective}} &= \frac{2}{3} \times Q \\
&= \frac{2}{3} \times 16.1 \\
\therefore Q_{\text{effective}} &= 10.73 \space Ahr
\end{aligned}
$$

### Evaluating Battery Life

Consider the battery-life formula:
$$
b = \frac{Q}{I}
$$

Where:
- $b \space (hr)$ is the battery life.
- $Q \space (Ahr)$ is the battery capacity.
- $I \space (A)$ is the current load.

The battery life for current draw when the mechatronic system is in use is:
$$
\begin{aligned}
b_{\text{load}} &= \frac{Q_{\text{effective}}}{I_{\text{effective}}} \\
&= \frac{10.73}{1.61} \\
\therefore b_{\text{load}} &= 6.66 \space hr
\end{aligned}
$$

The battery life for current draw when the mechatronic system is at rest is:
$$
\begin{aligned}
b_{\text{rest}} &= \frac{Q_{\text{effective}}}{I_{\text{rest}}} \\
&= \frac{10.73}{0.02} \\
\therefore b_{\text{load}} &= 536.5 \space hr
\end{aligned}
$$

### Evaluating Battery Requirements

Therefore, any rechargaeable battery that is capable of supplying at least $5 \space V$ and with a capacity of at least $10.73 \space Ahr$ is desired.

> If a battery has greater than $5 \space V$, then the voltage can be stepped-down with a buck converter.

> If a battery has less than $5 \space V$, then multiple batteries can be placed in series to increase the voltage or stepped-up with a boost converter.

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
    <tr>
        <td><a href="https://www.alibaba.com/product-detail/5v-3000mah-rechargeable-battery-3000-mah_62002339239.html">HW914067</a></td>
        <td>Lipo</td>
        <td>3000</td>
        <td>3.7</td>
        <td>5</td>
        <td>1</td>
        <td>1</td>
        <td>70 x 50 x 10</td>
        <td>500 - 1000</td>
    </tr>
</table>

> Manufacturers only manufacture batteries in multiples of $3.7 \space V$.

### Confirm Battery Discharge Current

The battery life of a single 105075 battery is:
$$
t = \frac{1}{Cr} = \frac{1}{0.2} = 5 \space hr
$$
- $t \space (hr)$ is the battery life.
- $Cr \space (hr^{-1})$ is the C-rate.

Consider Peukert's Law to determine there is sufficient current to power the mechatronic system:

$$
\begin{aligned}
C_{p} &= I^{k}t \\
\frac{2}{3} \times 5 &= I^{1.2} \times 1 \\
I_{\text{max}} &= 6.6 \space A > 1.61 \space A
\end{aligned}
$$

Where:
- $C_{p} \space (Ahr)$ is the capacity at one-ampere discharge rate.
- $I \space (Ahr)$ is the actual discharge current.
- $t \space (hr)$ is the time to discharge the battery.
- $k$ is the Peukert constant.

The discharge current of the battery is more than sufficient to power the mechatronic system.

> $k = 1.2$ is very modest for a lithium-ion polymer battery due to its "high" efficiency.

### Confirm Battery Energy

Consider the battery energy (which is effectively the energy discharged within one hour):
$$
\begin{aligned}
E_{\text{battery}} &= VQ_{\text{effective}} \\
&= 3.7 \times 10.73 \\
&= 39.701 \space Whr
\end{aligned}
$$

Where:
- $E \space (Whr)$ is the battery energy.
- $V \space (V)$ is the battery discharge voltage rating.
- $Q \space (Ahr)$ is the battery capacity.

### Confirm Battery Power

To confirm the battery has sufficient power to power the mechatronic system:
$$
P_{\text{battery}} = \frac{E_{\text{battery}}}{t} = \frac{39.701}{5} = 7.94 \space W
$$

Therefore:
$$
P_{\text{battery}} = 7.94 > 7.82 = P_{\text{mechatronic system}}
$$

The energy of the battery is more than sufficient to power the mechatronic system.

## Turbine Blade Design 💨

> Recall: $P_{\text{fluid}} = \frac{1}{2} \rho A v^3$.

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


### Rotor Solidity Factor

### Blade Aspect Ratio

### Rotor Swept Area

### Cut-In Wind Speed

Cut-in wind speed is the lowest wind speed for turbine to generate consistent power.

The turbine needs to generate enough starting torque at this wind speed to overcome its inertia.

> In a worst-case scenario, the motor could draw power from the battery to self-start the turbine.

### Cut-Out Wind Speed

Cut-out wind speed is the highest input wind speed that a turbine should generate consistent power for.

## Turbine Blade Material Selection 🍯



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