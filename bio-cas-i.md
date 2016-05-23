# BioCAS I

## Simultaneous monitoring of anesthetics and therapeutic compounds

### General Anesthesia

Today: How is anesthesia amount evaluated by the DOA? *A priori* predictive approach: pharmacokinetic models. Given some statistics about the patient, predict how much anesthesia is needed. *A posteriori* approach: Affected by artifacts, no control over plasma or effect site drug concentration.

### Feedback System

Program a pump to reach a certain level of patient sedation, use a continuous monitoring system to provide feedback about anesthesia concentration and sedation level. Hopefully this leads to a safer and more personalized way to introduce anesthesia.

Continuous drug monitoring is done with mass spectroscopy, liquid or gas chromatography, or an immunoassay, but these are technically not suitable for portable monitoring. Instead, electrochemical sensors are used. Electrochemical cells in a 3 electrode configuration: working electrode, counter electrode, and reference electrode. In particular, cyclic voltammetry is used because it is better for multiple drugs.

### System Architecture

Microcontroller is interfaced with the sensors with a voltage generating circuit and a current reading amplifier. Voltage ramp generator: drives the electrochemical cell.

### Results

Tested with propofol, paracetamol, and etoposide. There are very particular shapes and identifiable peaks in the IV curve for each drug (presumably presented individually), meaning that each can be identified individually. This work will hopefully be extended to analgesic and muscle relaxant compounds, providing complete control of anesthesia.

## A wireless tunable low drop-out regulator for subcutaneous muscle prosthesis

### Motivation

 - Existing issues for patients with limb loss
 - Proposed solution: Subcutaneous muscle prosthesis using iEAPs
 - Implantable integrated circuit stimulator module

2 million people in the US currently live with muscle loss. Existing solutions show contractility only after new muscle has been regenerated. New solutions are in demand to enable patients with immediate function. Artificial muscle: *ionic Electroactive Polymers* (iEAPs). Respond to electrical stimuli. Would like to develop a stimulator for an iEAP muscle prosthesis. Implantable stimulator: stable voltage needed for stimulating iEAPs, wireless tuning capability.

### Proposed wireless tunable LDO

 - LDO (low-dropout DC voltage regulator) integration challenges with iEAPs and the proposed solution
 - Wireless tuning technique

Design challenges: implantable electronics need to be low-power, high-integration; integration of LDO with iEAPs; WPT link powers up the LDO, line variation and high frequency noise; wireless tuning techniques are needed to change `Vout` of the LDO.

Proposed LDO (from previously published work, Y. Huang IEEE BioCAS 2015) external capacitor-less structure provided high integration, supported the wide load range of iEAPs.

### Circuit implementation

Frequency to current converter (FIC: generates a current proportional to the frequency of some input voltage (e.g. input voltage to input current). Reference adjuster: changes reference level and tunes LDO accordingly.

### Links

 - [Wikipedia page for EAPs](https://en.wikipedia.org/wiki/Electroactive_polymers)
