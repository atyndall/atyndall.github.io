---
layout: post
title: Research Proposal
category: articles
comments: true
tags: honours
---

This week I drafted and submitted my research proposal. Here is a copy converted to markdown. You can find the original in my [honours git repo](http://github.com/atyndall/honours).

# Non-Technical Summary
With the proportion of elderly and mobility-impaired people growing, and the cost of small computing platforms and sensors dropping, now more than ever we can create low-cost sensor systems to use in a "smart home for the disabled." One such sensor system is an occupancy sensor, which determines the number of people who are present in a given space. This has many applications in a such a smart home, like climate control, which studies have shown can be more efficient when computer controlled in this way.

This project will build on existing research to create an occupancy sensor and accompanying detection software that are well suited for a smart home for the disabled. This system will emphasise four key areas; low cost, non-invasiveness, energy efficiency and reliability. At the end of this project, a list of components and corresponding software will be produced, so that anyone can build the sensor prototype. The prototype will also be put to the test in real world situations around the UWA campus.

# Background
The proportion of elderly and mobility-impaired people is predicted to grow dramatically over the next century, leaving a large proportion of the population unable to care for themselves, and consequently less people able care for these groups. {% cite chan2009smart %} With this issue looming, investments are being made into a variety of technologies that can provide the support these groups need to live independent of human assistance. 

With recent advancements in low cost embedded computing, such as the [Arduino](http://arduino.cc/en/Guide/Introduction) and [Raspberry Pi](http://www.raspberrypi.org/), the ability to provide a set of interconnected sensors, actuators and interfaces to enable a low-cost "smart home for the disabled" is becoming increasingly achievable.

Sensing techniques to determine occupancy, the detection of the presence and number of people in an area, are of particular use to the elderly and disabled. Detection can be used to inform various devices that change state depending on the user's location, including the better regulation energy hungry devices to help reduce financial burden. Household climate control, which in some regions of Australia accounts for up to 40% of energy usage {% cite abs4602 %} is one particular area in which occupancy detection can reduce costs, as efficiency can be increased dramatically with annual energy savings of up to 25% found in some cases. {% cite erickson2013thermosense %}

Significant research has been performed into the occupancy field, with a focus on improving the energy efficiency of both office buildings and households. This is achieved through a variety of sensing means, including thermal arrays, {% cite beltran2013thermosense %} ultrasonic sensors, {% cite hnat2012doorjamb %} smart phone tracking, {% cite kleiminger2013using %}{% cite balaji2013sentinel %} electricity consumption, {% cite kleiminger2013occupancy %} network traffic analysis, {% cite ting2013occupancy %} sound, {% cite hailemariam2011real %} CO2, {% cite hailemariam2011real %} passive infrared, {% cite hailemariam2011real %} video cameras, {% cite erickson2013poem %} and various fusions of the above. {% cite yang2012multi %}{% cite ting2013occupancy %}


# Aim
While many of the above solutions achieve excellent accuracies, in many cases they suffer from problems of installation logistics, difficult assembly, assumptions on user's technology ownership and component cost. In a smart home for the disabled, accuracy is important, but accessibility is paramount.

The goal of this research project is to devise an occupancy detection system that forms part of a larger `smart home for the disabled' that meets the following accessibility criteria;

* **Low Cost**: The set of components required should aim to minimise cost, as these devices are intended to be deployed in situations where the serviced user may be financially restricted.
 
* **Non-Invasive**: The sensors used in the system should gather as little information as necessary to achieve the detection goal; there are privacy concerns with the use of high-definition sensors.
 
* **Energy Efficient**: The system may be placed in a location where there is no access to mains power (i.e. roof), and the retrofitting of appropriate power can be difficult; the ability to survive for long periods on only battery power is advantageous.
 
* **Reliable**: The system should be able to operate without user intervention or frequent maintenance, and should be able to perform its occupancy detection goal with a high degree of accuracy.

Success in this project would involve both

1. Devising a bill of materials that can be purchased off-the-shelf, assembled without difficulty, on which a software platform can be installed that performs analysis of the sensor data and provides a simple answer to the occupancy question, and
2. Using those materials and softwares to create a final demonstration prototype whose success can be tested in controlled and real-world conditions.

This system would be extensible, based on open standards such as REST or CoAP, {% cite guinard2012search %}{% cite kovatsch2013coap %} and could easily fit into a larger `smart home for the disabled' or internet-of-things system.

 
# Method
Achieving these aims involves performing research and development in several discrete phases.

### Hardware
A list of possible sensor candidates will be developed, and these candidates will be ranked according to their adherence to the four accessibility criteria outlined above. Primarily the sensor ranking will consider the cost, invasiveness and reliability of detection, as the sensors themselves do not form a large part of the power requirement.

Similarly, a list of possible embedded boards to act as the sensor's host and data analysis platform will be created. Primarily, they will be ranked on cost, energy efficiency and reliability of programming/system stability.

Low-powered wireless protocols will also be investigated, to determine which is most suitable for the device; providing enough range at low power consumption to allow easy and reliable communication with the hardware.

Once promising candidates have been identified, components will be purchased and analysed to determine how well they can integrate.

### Classification
Depending on the final sensor choice, relevant experiments will be performed to determine the classification algorithm with the best occupancy determination accuracy. This will involve the deployment of a prototype to perform data gathering, as well as another device/person to assess ground truth.

### Robustness / API
Once the classification algorithm and hardware are finalised, an easy to use API will be developed to allow the data the device collects to be integrated into a broader system.

The finalised product will be architected into a easy-to-install software solution that will allow someone without domain knowledge to use the software and corresponding hardware in their own environment.


# Timeline

| Date | Task |
|:-|:-|
| Fri 15 August | *Project proposal and project summary due to Coordinator* |
| August | Hardware shortlisting / testing |
| 25--29 August | *Project proposal talk presented to research group* |
| September | Literature review |
| Fri 19 September | *Draft literature review due to supervisor(s)* |
| October - November | Core Hardware / Software development |
| Fri 24 October | *Literature Review and Revised Project Proposal due to Coordinator* |
| November - February | *End of year break* |
| February | Write dissertation |
| Thu 16 April | *Draft dissertation due to supervisor* |
| April - May | Improve robustness and API  |
| Thu 30 April | *Draft dissertation available for collection from supervisor* |
| Fri 8 May | *Seminar title and abstract due to Coordinator* |
| Mon 25 May | *Final dissertation due to Coordinator* |
| 25--29 May | *Seminar Presented to Seminar Marking Panel* |
| Thu 28 May | *Poster Due* |
| Mon 22 June | *Corrected Dissertation Due to Coordinator* |


# Software and Hardware Requirements
A large part of this research project is determining the specific hardware and software that best fit the accessibility criteria. Because of this, an exhaustive list of software and hardware requirements are not given in this proposal.

A budget of up to $300 has been allocated by my supervisor for project purchases. Some technologies with promise that will be investigated include;

* **Raspberry Pi Model B+** Small form-factor Linux computer: Available from [here](http://arduino.cc/en/Guide/Introduction); $38

* **Arduino Uno** Small form-factor microcontroller: Available from [here](http://arduino.cc/en/Main/arduinoBoardUno); $36

* **Panasonic Grid-EYE** Infrared Array Sensor: Available from [here](http://www3.panasonic.biz/ac/e/control/sensor/infrared/grid-eye/index.jsp); approx. $33

* **Passive Infrared Sensor** Available from various places; $10-$20

# References
{% bibliography --cited %}