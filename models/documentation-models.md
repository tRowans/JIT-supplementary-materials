# Documentation For Blender Models File

- How to view models
- Map of models file
- Codes in the qubits-on-faces picture
- Defect deferral paths

## How To View Models

Extract the models.zip folder to get a models.blend file. To view the models you will need blender, which can be downloaded for free here. 

https://www.blender.org/

Viewing models will be easiest if you have a mouse with a clickable scroll wheel/middle mouse button. This will let rotate the camera by using middle mouse + moving the mouse and pan the camera using shift + middle mouse + moving the mouse. Otherwise you can rotate by clicking and dragging on the axes in the top right corner and pan and zoom using the two icons below them.

## Map of Models File

![Figure 1](https://github.com/tRowans/JIT-supplementary-materials/blob/main/models/map.jpg)

- A: Overlap of distance 3 slices in all three codes in the qubits-on-faces, qubits-on-edges and qubits-on-vertices pictures. 
- B: A distance 3 slice through the red code in the qubits-on-faces, qubits-on-edges and qubits-on-vertices pictures. A distance 3 layer in the red code in all three pictures. An exploded version of the slice in the qubits-on-faces picture showing the three independent layers.
- C: A defect deferral path in the red code in the qubits-on-vertices and qubits-on-faces pictures.
- D: A distance 3 slice through the blue code in the qubits-on-faces, qubits-on-edges and qubits-on-vertices pictures. A distance 3 layer in the blue code in all three pictures. An exploded version of the slice in the qubits-on-faces picture showing the three independent layers.
- E: Defect deferral paths in the blue code in the qubits-on-vertices and qubits-on-faces pictures.
- F: A distance 3 slice through the green code in the qubits-on-faces, qubits-on-edges and qubits-on-vertices pictures. A distance 3 layer in the green code in all three pictures. An exploded version of the slice in the qubits-on-faces picture showing the three independent layers.
- G: Defect deferral paths in the green code in the qubits-on-vertices and qubits-on-faces pictures.

## Codes in the Qubits-On-Faces Picture

### Red Code

This code is defined on a simple cubic lattice with qubits on faces, Z stabilisers on edges and X stabilisers on cells. An X error on a qubit violates the four Z stabilisers which form its perimeter, so the fact that syndromes for this error type form loops is immediately obvious in this picture. We are concerned only with Z stabilisers since our simulations only contain X errors. 

![Figure 2](https://github.com/tRowans/JIT-supplementary-materials/blob/main/models/red-code.png)

The left two figures show a single 2D code in the qubits-on-vertices and qubits-on-faces pictures. Z stabilisers are on hexagonal/half-hexagonal faces in the qubits-on-vertices picture. These are not stabiliser generators of the 3D code and so do not correspond to single edges in the qubits-on-faces picture. Two possible generating pairs/triples of these edges for each hexagon/half-hexagon are shown in red and blue in the middle figure. The figure on the right shows two adjacent layers (black and grey) which form a two-layer thick slice. The yellow highlighted edges correspond to the intermediate stabilisers between the two codes (which are stabiliser generators of the 3D code) and we can see that triples/pairs of these edges match the blue edge set in the black code and red edge set in the grey code. 

### Blue Code

![Figure 3](https://github.com/tRowans/JIT-supplementary-materials/blob/main/models/blue-code.jpg)

This is an exploded image of a slice in the blue code with qubits on faces (this 3D lattice is the rhombic dodecahedral lattice). From right to left we have the lower, middle and upper layers. It is very clear in this picture why slices must be three layers thick rather than 2. Shown in red are the edges where the middle layer meets the other two. Once again the Z stabilisers of the 2D codes (top and bottom layers) in this picture are not generators of the 3D code and instead correspond to sets of four edges (three red ones from the lower/upper layer and one perpendicular edge in the middle layer).

### Green Code

![Figure 4](https://github.com/tRowans/JIT-supplementary-materials/blob/main/models/green-code.jpg)

An exploded image of a slice in the green code. Shown in black (blue) are the edges where the bottom (top) layers meet the middle layer. Unlike in the previous examples the Z stabilisers in the 2D codes corresponding to the top and bottom layers are weight-3 and are stabilisers of the 3D code (the grey edges). 

## Defect Deferral Paths

NOTE: "Defects" here are what are referred to as "endpoints" in the main paper.

For the delayed matching decoder to work we need the matching of defects to the top facet of a slice to result in an equivalent pair of defects in the next slice if this matching was incorrect and the defects should have been matched to each other. As described in the main paper, deferral of defects is a result of an erroneous correction to the top facet which creates a syndrome + the fact we assume all bottom facet Z stabilisers are in the +1 eigenstate. (in the qubits-on-vertices picture) This means we can only defer into cells at the bottom of the new slice which share a stabiliser with the old slice and cannot defer general defects from one slice into the corresponding position in the next slice. This is not a serious issue because we can simply defer all defects into these bottom cells, and while for some defects this will differ from their position in the previous slice they will also be deferred to bottom cells in all future slices so errors grow only by a constant amount due to this.

### Red Code

As usual this is the simplest case. There are faces in this lattice (in the qubits-on-vertices picture) which are normal to the time direction for the code (in the qubits-on-vertices picture these are edges parallel to the time direction) so we simply need to flip a line of these until we reach the top. Defects in bottom cells require two flipped faces whereas those in middle cells only require one. For top cells one of the faces is a hexagonal face of the top 2D code and since this is not a stabiliser generator we cannot detect defects in these cells and the value of this hexagonal stabiliser is whatever is necessary to produce a valid syndrome in the cell (technically this is true for bottom cells as well but because we assume we have successfully corrected the previous slice we assume all generators for the bottom cell hexagonal stabilisers are in the +1 eigenstate).

### Blue Code

There are no faces normal/edges parallel to the time direction in the rhombic lattices so paths are more complicated. The paths shown in the .blend file are not unique and there exist other valid paths, but these ones have the advantages of being of minimum length and being valid for all vertices in the lattice. They are (maximum) length 4 as opposed to the (maximum) length 2 path for the red code so involves one bottom cell and three other cells, one of which is a top cell which, as with the red code, does not allow detection of defects.

### Green Code

Unlike in the previous two cases the Z stabilisers of the 2D codes on the faces of this slice are stabiliser generators of the 3D code so defects in top cells can be detected. Additionally, there are two types of cell which meet these boundaries (octahedral and cuboctahedral) and we need to make sure that defects from each type are deferred to the same type. For example, the cuboctahedral cells have faces on both the top and bottom boundaries but if a defect begins in this cell we cannot defer it straight through the top face because the cell on the other side in the next slice is an octahedral cell. The models show a valid choice of path for octahedral cells in blue and cuboctahedral cells in red. 


