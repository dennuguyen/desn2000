# Define 📚

Translation of user-focused thinking to technical-focused thinking.

> CN: Customer needs

> FR: Functional requirements

## Work Packages 💼

[TOC]

## Affinity Map CN to FR 🗺

Translating CN to FR lets us shift our user-focused thinking into technical-focused thinking.

Customer needs **are** requirements. However, customer needs may not cleanly translate to the solution which is why functional requirements need to be developed. The tool we use to deduce what our functional requirements are is affinity mapping (which is a method of categorisation).

From our list of customer needs (from this [Google Doc](https://docs.google.com/document/d/1A06ONjj7tLm_xGvUQfQnWL-As_b0yvIB1bE-RqM8eos/edit), we categorised the customer needs into general requirements. This is the first draft:

![image](affinity-map-cn-to-fr-1.png)

We further refined the affinity map into the following as we fleshed out the categories into root functional requirements:

![image](affinity-map-cn-to-fr-2.png)

There was a clean trend where `sustain` was closely related to constraints and `improve` was closely to functional requirements.

```mermaid
graph LR
    US1[As a resident, I want my current lifestyle to be maintained, as I am content with the status quo.]
    US2[As a resident, I want to be able to cool down in the summer, so I do not feel uncomfortable and exhausted.]
    US3[As a resident, I do not want to pay for the cost of implementing any solutions, as I am saving up my money for other investments.]
    US4[As a resident, I want to pay low electricity utilities, as I am saving up my money for other investments.]
    US5[As a building owner, I want to lower my electricity utility bills, so I can save money.]
    US6[As a ventilation company CEO, I want an eco-friendly ventilation system, so I can out-compete other ventilation companies.]
    US7[As a ventilation company CEO, I want more work, so I can make profits.]
    US8[As a city planner, I want to implement urban environment cooling solutions, so I can mitigate the impact of the heat island effect in my community.]
    US9[As a city planner, I want to lower the cost of utilities for my community, so they can save money for other needs or comforts.]
    US10[As an environmentalist, I want to implement urban environment cooling solutions, so I can mitigate the effects of climate change.]

    US1 --> CN2
    US2 --> CN1
    US2 --> CN2
    US3 --> CN6
    US4 --> CN6
    US5 --> CN6
    US6 --> CN5
    US6 --> CN6
    US6 --> CN7
    US7 --> CN5
    US7 --> CN7
    US8 --> CN1
    US8 --> CN2
    US9 --> CN6
    US10 --> CN3
    US10 --> CN4

    CN1[Cooling]
    CN2[Lifestyle]
    CN3[Energy]
    CN4[Environment]
    CN5[Infrastructure]
    CN6[Cost]
    CN7[Business]
```

## FR Hierarchy 🌳

Decomposition of the highest-level FR into lower-level FRs.

The root functional requirements that we have identified were:
- Protect the environment.
- Harvest wasted energy.
- Mitigating heat footprint.
- Save money.

The root constraints that we have identified were:
- Minimise economic impact.
- Minimise impact on existing infrastructure.
- Maintain lifestyles of current building inhabitants.
- Minimise impact on business/jobs.

The next step is to decompose the above requirements (green are functional requirements, blue are constraints):

![image](fr-hierarchy.png)

```mermaid
graph LR
    subgraph Sustain
        DC1[Minimise economic impact.]
        DC2[Minimise impact on existing infrastructure.]
        DC3[Maintain lifestyles of current building inhabitants.]
        DC4[Minimise impact on business/jobs.]
        DC5[Mitigate impact on environment.]
    end

    subgraph Improve
        FR1[Harvest wasted energy.]
        FR1[Decrease d.]
    end
```

## Problem Area Research 🧐

### Gathering Field Data 🏑

First-hand data helps to inform what the FR metrics should be.

We gathered first-hand data by finding AC ventilation and measuring the temperature and airflow.

<table>
    <tr>
        <th>Date</th>
        <td>2022/09/06, 1800</td>
    </tr>
    <tr>
        <th>Weather</th>
        <td>19 °C, 0 m/s winds</td>
    </tr>
    <tr>
        <th>Location</th>
        <td>6/180 Thomas St, Haymarket</td>
    </tr>
</table>


![image](6-180-thomas-1.png)

<table>
<thead>
<tr>
    <th>Location</th>
    <th>Temperature (°C)</th>
    <th>Airflow (m/s)</th>
    <th>Average Temperature (°C)</th>
    <th>Average Airflow (m/s)</th>
</tr>
</thead>
<tbody>
<tr>
    <td rowspan="3">L1<br>(Control)</td>
    <td>19.4</td>
    <td>0.00</td>
    <td rowspan="3">19.4</td>
    <td rowspan="3">0.00</td>
</tr>
<tr>
    <td>19.4</td>
    <td>0.00</td>
</tr>
<tr>
    <td>19.4</td>
    <td>0.00</td>
</tr>
<tr>
    <td rowspan="6">L2</td>
    <td>21.1</td>
    <td>1.58</td>
    <td rowspan="6">21.47</td>
    <td rowspan="6">1.43</td>
</tr>
<tr>
    <td>21.0</td>
    <td>1.35</td>
</tr>
<tr>
    <td>21.8</td>
    <td>1.20</td>
</tr>
<tr>
    <td>21.8</td>
    <td>1.21</td>
</tr>
<tr>
    <td>21.6</td>
    <td>1.57</td>
</tr>
<tr>
    <td>21.5</td>
    <td>1.64</td>
</tr>
<tr>
    <td rowspan="7">L3</td>
    <td>21.5</td>
    <td>1.54</td>
    <td rowspan="7">21.4</td>
    <td rowspan="7">1.69</td>
</tr>
<tr>
    <td>21.5</td>
    <td>1.75</td>
</tr>
<tr>
    <td>21.1</td>
    <td>1.57</td>
</tr>
<tr>
    <td>21.1</td>
    <td>1.30</td>
</tr>
<tr>
    <td>21.5</td>
    <td>1.82</td>
</tr>
<tr>
    <td>21.4</td>
    <td>1.67</td>
</tr>
<tr>
    <td>21.7</td>
    <td>2.18</td>
</tr>
<tr>
    <td rowspan="7">L4</td>
    <td>21.8</td>
    <td>1.21</td>
    <td rowspan="7">21.27</td>
    <td rowspan="7">1.24</td>
</tr>
<tr>
    <td>21.3</td>
    <td>1.23</td>
</tr>
<tr>
    <td>21.7</td>
    <td>1.30</td>
</tr>
<tr>
    <td>21.3</td>
    <td>1.35</td>
</tr>
<tr>
    <td>21.3</td>
    <td>0.98</td>
</tr>
<tr>
    <td>21.1</td>
    <td>1.33</td>
</tr>
<tr>
    <td>20.4</td>
    <td>1.31</td>
</tr>
</tbody>
</table>

The [recommended internal building temperature](https://www.designingbuildings.co.uk/wiki/Temperature_in_buildings) is 21 °C for thermal comfort. It is clear to see that the exhausted air temperature is close.

<table>
<thead>
<tr>
    <th>Location</th>
    <th>Temperature Difference Between Control and Building (°C)</th>
    <th>Airflow Difference Between Control and Building (m/s)</th>
</tr>
</thead>
<tbody>
<tr>
    <td>L2</td>
    <td>2.07</td>
    <td>1.43</td>
</tr>
<tr>
    <td>L3</td>
    <td>2.00</td>
    <td>1.69</td>
</tr>
<tr>
    <td>L4</td>
    <td>1.87</td>
    <td>1.24</td>
</tr>
<tr>
    <td>Average</td>
    <td>1.98</td>
    <td>1.45</td>
</tr>
</tbody>
</table>

Summarised image (green is control data, red is independent data, blue is building):

![image](6-180-thomas-2.png)

### HVAC Systems Research 💨

### Ventilation Flow Rate 🎏

```math
```

Where:
- $``$ is the .

### Turbelence 🏸

[Turbelence is a fluid motion characterised by chaotic changes in pressure and flow velocity](https://en.wikipedia.org/wiki/Turbulence).

Turbelence is characterised by:
- Irregularity.
- Diffusivity.
- Rotationality.
- Dissipation:

Turbelence can be predicted by the Reynolds number (the larger the number, the more likely turbelence will occur):

```math
\text{Re} = \frac{\rho v L}{\mu}
```

Where:
- $`\rho`$ is the fluid density $`(kg/m^3)`$.
- $`v`$ is the fluid velocity $`(m/s)`$.
- $`L`$ is the linear dimension $`(m)`$.
- $`\mu`$ is the fluid dynamic viscosity $`(Ns/m^2)`$.

## Defining FR Metrics 💯

The definition of metrics helps specify the FR.

## Defining Design Constraints 🛑

## Requirements Diagram

```mermaid
requirementDiagram
    functionalRequirement Harvest Wasted Energy {
        id: 1
        text: Harvest wasted energy from building ventilation systems.
        risk: high
        verifymethod: demonstration
    }

    functionalRequirement Harvest Exhausted Air {
        id: 1.1
        text: Harvest exhausted air from building ventilation.
        risk: high
        verifymethod: analysis
    }

    functionalRequirement Harvest Wind Energy {
        id: 1.1.1
        text: Harvest wind energy.
        risk: high
        verifymethod: analysis
    }

    functionalRequirement Turbulence {
        id: 1.1.1.1
        text: Withstand turbulent airflow where Reynolds number ranges from 30000 and 60000.
        risk: low
        verifymethod: analysis
    }

    functionalRequirement Wind Direction {
        id: 1.1.1.2
        text: Harvests wind energy from different wind directions.
        risk: low
        verifymethod: test
    }

    functionalRequirement Air Flow {
        id: 1.1.1.3
        text: Able to operate in air flow between 1400 and 1600 L/s.
        risk: high
        verifymethod: test
    }

    functionalRequirement Noise {
        id: 1.1.1.5
        text: Harvest wind energy with minimal noise pollution.
        risk: low
        verifymethod: analysis
    }

    functionalRequirement Wake {
        id: 1.1.1.6
        text: Output Reynolds number is less than 60000.
        risk: low
        verifymethod: analysis
    }

    functionalRequirement Output Air Velocity {
        id: 1.1.1.7
        text: Output air velocity is more than 3 m/s.
        risk: low
        verifymethod: analysis
    }

    functionalRequirement Store Energy {
        id: 1.2
        text: Store energy.
        risk: high
        verifymethod: analysis
    }

    functionalRequirement Use Energy {
        id: 1.2.1
        text: Ensure stored energy can be used later.
        risk: low
        verifymethod: analysis
    }

    functionalRequirement Convert Energy {
        id: 1.3
        text: Convert energy into electricity.
        risk: low
        verifymethod: analysis
    }

    functionalRequirement Power {
        id: 1.3.1
        text: Can power electronics at an average power of 3 W.
        risk: low
        verifymethod: analysis
    }

    Harvest Wasted Energy -derives-> Harvest Exhausted Air
    Harvest Wasted Energy -derives-> Store Energy
    Harvest Wasted Energy -derives-> Convert Energy
    Harvest Exhausted Air -derives-> Harvest Wind Energy
    Harvest Wind Energy -derives-> Turbulence
    Harvest Wind Energy -derives-> Wind Direction
    Harvest Wind Energy -derives-> Air Flow
    Harvest Wind Energy -derives-> Noise
    Store Energy -derives-> Use Energy
    Convert Energy -derives-> Power
```