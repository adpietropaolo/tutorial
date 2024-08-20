#PLUMED Tutorial on Trans-Cis isomerization in the ground and excited states

This lesson intends to show ho to combine PLUMED with your MD code to simulate dihedral angle isomerization in ground and excited states using FEP and Hamiltonian Replica exchange.
In this tutorial you will find:
*The reference paper.
*The slides of the simulation workflow.
*The instructions on how to setup the simulations.
*The plumed input file.
*A python notebook with a solution useful to complete the exercise.

```mermaid
flowchart LR
A[The method intro] ==> B[Lecture I]
B ==> C[The lecture slides]
C ==> D[Instructions]
D ==> E[solution]
click A "mypaper" "The paper related to the Multi-replica biased sampling for Trans-cis isomerization in the ground and excited states using PLUMED"
click B "Slide.pdf" "The lecture slides"
click C "README.md" "The instructions for the masterclass"
click D "plumedfile.md" "The example plumed input file"
click E "notebook.ipynb" "The notebook file"
```