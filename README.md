# PD-SoC-Design
The phase of the computer chip creation process where the precise physical architecture of the circuitry is decided upon is referred to as physical design. To put it another way, it's similar to creating the schematic or map that shows how all the tiny electronic parts (such as wires and transistors) are going to be placed on a computer chip.
Welcome to the PD-SoC-Design wiki!
* * Welcome to the workshop for OpenLane. We will explore the process of creating an Application Specific Integrated Circuit (ASIC) using the OpenLane ASIC flow, starting from the Register Transfer Level (RTL) and ending with the Graphical Data System (GDS) file. The process consists of multiple essential phases, commencing with an RTL file and concluding with a GDS file.

-------------------------------------------------------------------------------------------------------------------------------------------------------
Topics we cover 👍 

1) Comprehending the RTL to GDS Process:

Understood how to translate a high-level hardware description into a practical ASIC architecture from start to finish. acknowledged the significance of every phase in the process, from synthesis to approval.

2) Synthesis: Discovered how to use common cell libraries to transform RTL into a gate-level netlist. determined the various cell perspectives (Liberty, HDL, SPICE, Layout).

3)Floor and Power Planning: Understood the significance of floor planning in chip partitioning and I/O pad placement.

-------------------------------------------------------------------------------------------------------------------------------------------------------

In VLSI design, the RTL to GDSII pipeline transforms an RTL description of a digital circuit into a physical layout that is prepared for production. It goes through several steps, including RTL synthesis, floor planning, placement, routing, and the creation of the GDSII file format, which is where the layout data is eventually included. This methodical procedure guarantees that the final IC layout precisely matches the intended functionality and satisfies manufacturing specifications.
 *
*Picture of VSD Squadron:
<img width="599" alt="vsd squadron" src="https://github.com/user-attachments/assets/1ae35eef-52fb-420c-ac24-af3f5b02bc73">


Intorduction:

ISA: "Instruction Set Architecture" is what ISA stands for.It's just a way to communicate with the computer. Generally speaking, we develop programs that need to be executed by the system using coding languages like C, Java, and others; however, machines cannot understand these languages. This is where ISA comes into play. ISA will be used to convert the written codes from assembly language to binary, or machine-readable language. For this purpose, the most recent ISA to be disclosed is the RISC V ISA.

-------------------------------------------------------------------------------------------------------------------------------------------------------

RTL Designs: What Are They?

A crucial stage in the VLSI design flow is RTL (Register-Transfer-Level) design, which focuses on building electronic circuits utilizing integrated circuits (ICs). By outlining the digital signal flow between hardware registers and the logical operations carried out on these signals, it describes a digital circuit. EDA Tools: What Are They?

Software programs called EDA (Electronic Design Automation) tools are used to design and test integrated circuits (ICs). They make that the integrated circuit satisfies the necessary performance and density requirements. PDK Data: What Is It?

During IC design, a set of files called the Process Design Kit (PDK) is utilized to simulate the fabrication process for EDA tools. This package contains:

Process Design Rules: PEX (Parasitic Extraction), LVS (Layout Versus Schematic), and DRC (Design Rule Check)

RTL to GDS Flow: 

Through a series of steps, the simplified RTL to GDS pipeline starts with an RTL file and ends with a GDS file that can be delivered to a foundry for fabrication. The following are the steps in the RTL to GDS flow:

https://images.app.goo.gl/ZS34Yp7621rUxnxPA[RTL 2 GDS]
-------------------------------------------------------------------------------------------------------------------------------------------------------
Stythesis in OpenLane: 

Synthesis: Parts from the Standard Cell Library are used to turn the RTL file into a circuit.
    The library's Standard Cells are arranged in a standard manner, with varying widths but the same height.
    Different models based on electrical, HDL, Spice, and layout (abstract and detailed) factors are used for each cell.
<img width="906" alt="synthesis" src="https://github.com/user-attachments/assets/6b22608a-eac2-4a39-9930-8ede89df61d7">
----

----
image::https://images.app.goo.gl/cwsFBX2pdMvjG2mV8[Synthesis flow in VLSI]

Floor plan: 
In hierarchical processes, floorplanning offers a foundation for determining when the top level will occur. The clock cycle time is assigned to each block in a timing budget based on the top-level timing estimate. Timing closure is ensured by an efficient floorplan, which does this by arranging blocks to shorten essential paths, avoiding routing congestion that would result in longer paths, and removing the requirement for excessive routing for noise-sensitive blocks. The difficult part of designing a floor plan is making sure that there is enough room for standard cell placement, signal and clock routing, and high area efficiency.

The dimensions and form of the chip or block are specified in the floorplan. Placement of IO and macro cells is being done so that effective routing space is accessible both between the macro and IO sections as well as between the channel region. We preserve the contiguous core area from the target cell library for standard cell placement and optimization technique.

<img width="928" alt="run floorplan " src="https://github.com/user-attachments/assets/ede7e193-1459-451b-bca4-cd03deea1566">


Placement :

From the floor planning phase forward, components are positioned within the allocated spaces.
    Within their cell boundaries are also the Standard Cells that are necessary for the design.
    There are two stages to placement: Global Placement, in which cells may overlap, and Detailed Placement, in which cells are arranged according to placement principles to create the best possible placement.
    
<img width="599" alt="placement theory" src="https://github.com/user-attachments/assets/03038995-0735-4bc3-8439-a89ca33cf119">

<img width="926" alt="placement magic-T" src="https://github.com/user-attachments/assets/1aa8f6ca-4837-4b0a-82fb-10a3714d85c7">

image::https://images.app.goo.gl/Vqz5wU7WdAnk41Q47[placement image]


CTS(Clock tree synthesis):

A method for dividing the clock equally across each successive component of a VLSI design is called clock tree synthesis. Clock Tree Synthesis is used to minimize delay and skew. The clock tree limits and the placement data are supplied as input to Clock Tree Synthesis.

<img width="926" alt="cts magic-T" src="https://github.com/user-attachments/assets/91cbdc4e-374e-4869-ba29-fbf4cca2814e">

image::https://images.app.goo.gl/gNDyWN1t1Hg6g6hj7[Design before CTS]
image::https://images.app.goo.gl/rSGBd4BdLyoNv2Un6[Design after CTS]

Routing : 

Routing is the stage after Clock Tree Synthesis and optimization where-

Exact paths for the interconnection of standard cells and macros and I/O pins are determined.
Electrical connections using metals and vias are created in the layout, defined by the logical connections present in the netlist.
After CTS, we have information of all the placed cells, blockages, clock tree buffers/inverters and I/O pins. The tool relies on this information to electrically complete all connections defined in the netlist such that-

* There are minimal DRC violations while routing.
* The design is 100% routed with minimal LVS violations.
* There are minimal SI related violations.
* There must be no or minimal congestion hot spots.
* The Timing DRCs are met.
* The Timing QoR is good.

<img width="925" alt="routing console" src="https://github.com/user-attachments/assets/2e021b9c-6f54-44ff-99c6-0ecf149e44cf">
<img width="869" alt="routing 1" src="https://github.com/user-attachments/assets/1ff66fe7-361e-4b22-b581-b21c86dabed5">
<img width="929" alt="routing 2" src="https://github.com/user-attachments/assets/79d6b4ad-6ce2-4d25-99fd-7f4eb1913b5e">
<img width="929" alt="after routing " src="https://github.com/user-attachments/assets/7b8cd3f7-c89d-4425-9b0b-bd5a777cbeee">

image::https://images.app.goo.gl/33653N2Xt33wLs9A9[Routing image]


