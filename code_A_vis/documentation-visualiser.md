# Documentation For Visualiser Output File

The slides in code_A_vis.pdf show visualisations of the numerical simulations used to obtain the threshold plots in the main text. This specific case is an L=10 slice through code A for p=0.005. The parameters for the delayed matching decoder (as defined in the main text) are c=2 and r=1. The bottom, middle and top layers of this slice are shown respectively on each slide from left to right. These layers are shown in the qubits-on-faces picture, and so will be easiest to understand if you have already read the "documentation-models.md" file and viewed the 3D models which explain the slices in this picture. The deferral paths of the defects (syndrome endpoints) are also explained there. 

The visualised simulation is for 15 "expand -> decode -> collapse" cycles + a step at the end which projects to the codespace of a final 2D layer to check for uncorrectable errors. Each of these cycles consists of the following steps

- calculate syndrome for the errors in the slice
- apply measurement errors to this syndrome with probability p
- find the defects in this syndrome
- apply JIT decoding to repair this syndrome
- use the sweep decoder to find a data qubit correction based on the repaired syndrome
- apply data qubit errors to the top layer with probability p

We then proceed to the next slice, with the top layer of the previous slice becoming the bottom layer of this new one.

We now justify a few simplifications made in this simulation: 

Firstly, in practise the measurement of Z stabilisers to expand from 2D -> 3D would result in a random distribution of X errors on the new qubits of the slice (i.e. those which are not part of the bottom layer). In the absence of measurement errors on the newly measured stabilisers or data qubit errors on the bottom code, the decoding of this random error distribution will always succeed. In the presence of one or both of these additional error types it can fail, but the defect configurations created by a given measurement error/bottom code data error are independent of the random error distribution produced by stabiliser measurements, and the data qubit error which results from a failed application of the JIT decoder + sweep is also independent of this initial configuration. Thus, for our simulation it is sufficient to post-select on the zero-error case when expanding the slice.

Secondly, X errors on data qubits can occur at any point after stabiliser measurement but before the collapse of the slice. However, because all the operations we apply in the simulation (repair of the syndrome and application of an X correction) commute with these random X errors it is sufficient to apply them all the end, just before collapse. We only apply the errors to the top layer because the other two are discarded in the next step.  
