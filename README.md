# RISC-V-tapeout-Program-Week-4
Lets's Forwarding to the RISC-V journey, Week 4 deals with the CMOS circuit design and simulation using SPICE software.

### DAY 1
Day 1 deals with the basics of circuit design and the SPICE simulation.

* Need of SPICE

     - SPICE stands for Simulation Program with Integrated Circuit Emphasis. SPICE is used to calculate the delay of the circuit using waveforms. If there is no delay then there will be no physical design.
     - SPICE allows you to simulate how your circuit will respond to different inputs (DC, AC, transient, noise, etc.)
     - SPICE lets you test various design options virtually, identify problems early, and minimize the need for multiple prototypes.
SPICE have predfefined models which are need to be correctly defined for the particular requirement of the designer.

* Cicuit Design : CMOS circuit is composed of combination of NMOS and PMOS which are complementary of each other.

     - NMOS (N-type metal oxide semiconductor): NMos is a 4 terminal device. NMOS structure is composed of: 

               * Isolation region (SiO2) which is used to differentiate between the adjacent transistors.
       
               * n+ Diffusion region

               * Gate Oxide

               * Poly-Si or Metal Gate

               * Gate, Source, Drain, Body

               * NMOS works in three regions: Cutoff, Resistive or linear, Saturation

               * Cutoff region: The cutoff region is the “OFF” state of an NMOS transistor — no current flows from drain to source because the channel has not yet formed. Here Vgs-Vt<0).

       <img width="788" height="693" alt="Screenshot 2025-10-17 073959" src="https://github.com/user-attachments/assets/53eb7496-2cdb-49ba-bbc5-6edd4c4c6982" />


    - Threshold Voltage: The threshold voltage (Vₜ) is the minimum gate-to-source voltage at which a MOSFET begins to conduct or it can be defined as the voltage required to invert the channel.

               * Case 1: If Vgs=0, Drain, source, body/substrate are connected to ground (GND) then substrate-source (B-S) and Substrate - Drain (B-D) form pn junction diode. here both the junctions are off due to 0V bias and the source to drain resistance is high. It is the cutoff region where Vgs < Vt.

               * Case 2: Apply positive Vgs voltage. This causes the oxide to acts as a dielectric and form capacitor. Mobile holes under the gate get repellled by the positive charge at G and leave behind the negative charge. It leads to accumulation of negative charge under the gate.
 
  <img width="1230" height="713" alt="Screenshot 2025-10-17 074822" src="https://github.com/user-attachments/assets/e24702f9-92a6-45d1-853a-a572f497a1eb" />


               * Case 3: Increase the Gate voltage Vgs. Now more number of charges get repelled and the depletion width increases. Now it leads to the inversion at the semiconductor surface to n-type.This phenomena is called strong inversion. The Vgs voltage at which strong inversion occur is called thresold voltage (Vt).

<img width="1202" height="692" alt="Screenshot 2025-10-17 075237" src="https://github.com/user-attachments/assets/ef5b85d4-5244-4d67-91f9-bb587752c716" />


               * Case 4: Further increase in Vgs leads to the attraction of negative charge carriers from n+ region.It leads to no change in the depletion width. Hnece the continuous n-channel formation from souce- Drain takes place which is modulated by Vgs.

               * Note: Body terminal plays a crucial role in tuning the threshold voltage. If biasing is applied between souce and body then it increases the depletion width near the source region. Therefore in the circuit inversion is delayed by Vsb beacuse negative charges get attracted towards the positive terminal of souce due to Vsb and leads to body current. Hence the semiconductor surface inverts the n-type material at a voltage Vgs= Vt0 +V

               * Threshold Voltage Equation: 
               
<img width="700" height="334" alt="Screenshot 2025-10-18 063833" src="https://github.com/user-attachments/assets/68449ec6-0e7c-4517-a4e6-dc468bb11914" />


    - Resistive Operation: 
The linear region, also called the resistive region, is where the NMOS transistor is ON and behaves like a voltage-controlled resistor — current flows easily from drain to source.
It occur when Vgs>Vt. As the Vgs increases depletion width increases and hence in the channel charge is induced which is directly proportional to the Vgs-Vt. 

              * There two types of current: Drift current : It is the current due to potential difference. Drift current is calculated as the velocity of change carrier and the available charge over channel width.  Drain current is given as :
              
<img width="666" height="794" alt="Screenshot 2025-10-17 084723" src="https://github.com/user-attachments/assets/5e7d6ecd-cfcb-44a4-8f0f-11cdd20f0ea3" />
<img width="613" height="79" alt="Screenshot 2025-10-17 085032" src="https://github.com/user-attachments/assets/2f3e3438-8713-4f75-84d6-8cb8a92627fe" />


              * Diffusion current: This current arises due to the difference in the carrier concentration.
    - Saturation Region
Saturation happens when Vgs-Vds<Vt. here is no channel near the drain. This region is called pinch off region. Here the current flows but its linarity gets change. 

<img width="1070" height="865" alt="Screenshot 2025-10-17 091809" src="https://github.com/user-attachments/assets/dd10de7a-56d8-499c-8faa-a9774d57cddb" />

Saturation current is given as :

<img width="540" height="132" alt="Screenshot 2025-10-18 063842" src="https://github.com/user-attachments/assets/9b9d1322-6200-4bf2-9e07-52f55a5b191b" />


* Introduction to SPICE
  Spice is a simualtion tool which have pref=defined models. Steps to done in SPICE are:
      - Define the SPICE Model Parameters

      - Create SPICE Netlist: NMOS spice netlist is looks like:

                      - M1 vdd n1 0 0 nmos W=1.8u L=1.2u where Mxx=MOSFETxx, vdd= Drain, n1-Gate, 0=source, 0=body these are the nodes.

                      - R1 in n1 55 where in is the first terminal, n1 is the second terminal, 55 is the value of resistance

                      - Vdd vdd 0 0.25 where Vxx=Voltage source, vdd is positive terminal, 0 is the negative terminal

                      - Vin in 0 2.5

         Next step is to define technology parameters. Model parameters for nmos are Vt0, Gamma, Kn', lambda.

         .MODEL nmos NMOS (TOX=.. +VTH0=.. U0=.. Gamma1=..)=> package this file into .mod file like xxxx_025um_mode1.modand now include this file using :

         .LIB "xxxx_025um)mode1.mod" CMOS_MODELS

          Next is the simulation command step which is used to describe how to apply the voltages and the sweep of Vgs and Vds.

<img width="806" height="576" alt="Screenshot 2025-10-17 221325" src="https://github.com/user-attachments/assets/47d5ca95-9f4a-42c7-a1bb-08f431f813da" />
<img width="800" height="296" alt="Screenshot 2025-10-17 222003" src="https://github.com/user-attachments/assets/237c1986-ad7d-4ffa-9c84-4c2ee053d3ac" />

<img width="1604" height="774" alt="Screenshot 2025-10-17 222205" src="https://github.com/user-attachments/assets/60004206-3d82-44cf-beaf-6beecf4e30e5" />
<img width="1168" height="842" alt="Screenshot 2025-10-17 222333" src="https://github.com/user-attachments/assets/fd439eba-edae-4008-a801-2dc0f5a58597" />
<img width="1711" height="1005" alt="Screenshot 2025-10-17 222430" src="https://github.com/user-attachments/assets/7a6db1dc-49bb-49c4-8aff-5b9b3ff93e34" />
<img width="421" height="248" alt="Screenshot 2025-10-17 222452" src="https://github.com/user-attachments/assets/588d40c8-5912-4cf3-9384-99e395093523" />

