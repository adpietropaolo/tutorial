```plumed
#SOLUTIONFILE=https://github.com/adpietropaolo/tutorial/blob/main/plumed.dat

WHOLEMOLECULES STRIDE=1 ENTITY0=1-347




TORSION ATOMS=4,3,84,85    LABEL=T1   
TORSION ATOMS=74,73,153,154  LABEL=T2
TORSION ATOMS=143,142,222,223 LABEL=T3
TORSION ATOMS=212,211,280,293  LABEL=T4     


# this the lambda value for current window
lambda1: CONSTANT VALUE=0.00
lambda2: CONSTANT VALUE=0.0



# first we define V0 for T1, which is the torsional potential in the ground state for the dihedral angle T1
MATHEVAL ...
 LABEL=V0_1 ARG=T1 VAR=x
 FUNC=12.16-0.024*cos(x-pi)-43.32*(cos(x-pi))^2+0.12*(cos(x-pi))^3+38.8*(cos(x-pi))^4-0.0601*(cos(x-pi))^5
 PERIODIC=NO
... MATHEVAL

# then V1 for T1, which is the torsional potential in the first excited state for the dihedral angle T1
MATHEVAL ...
 LABEL=V1_1 ARG=T1 VAR=x
 FUNC=301.3-0.1478*cos(x-pi)-48.16*(cos(x-pi))^2+0.9948*(cos(x-pi))^3+34.30*(cos(x-pi))^4-1.001*(cos(x-pi))^5
 PERIODIC=NO
... MATHEVAL


# then V2 for T1, which is the torsional potential in the second excited state for the dihedral angle T2
MATHEVAL ...
 LABEL=V2_1 ARG=T1 VAR=x
 FUNC=348.8-0.1104*cos(x-pi)-54.71*(cos(x-pi))^2+0.7533*(cos(x-pi))^3+35.14*(cos(x-pi))^4-0.8068*(cos(x-pi))^5
 PERIODIC=NO
... MATHEVAL


# You can then continue with biasing the potential for as many torsions if you want


# We can define V0 for T2
MATHEVAL ...
 LABEL=V0_2 ARG=T2 VAR=x
 FUNC=12.16-0.024*cos(x-pi)-43.32*(cos(x-pi))^2+0.12*(cos(x-pi))^3+38.8*(cos(x-pi))^4-0.0601*(cos(x-pi))^5
 PERIODIC=NO
... MATHEVAL

# then V1 for T2
MATHEVAL ...
 LABEL=V1_2 ARG=T2 VAR=x
 FUNC=313.9+0.3972*cos(x-pi)-72.12*(cos(x-pi))^2-0.9463*(cos(x-pi))^3+43.87*(cos(x-pi))^4+0.5858*(cos(x-pi))^5
 PERIODIC=NO
... MATHEVAL


# then V2 for T2
MATHEVAL ...
 LABEL=V2_2 ARG=T2 VAR=x
 FUNC=351.9-0.7135*cos(x-pi)-69.01*(cos(x-pi))^2+0.653*(cos(x-pi))^3+47.11*(cos(x-pi))^4+0.41*(cos(x-pi))^5
 PERIODIC=NO
... MATHEVAL



# We can define V0 for T3
MATHEVAL ...
 LABEL=V0_3 ARG=T3 VAR=x
 FUNC=12.16-0.024*cos(x-pi)-43.32*(cos(x-pi))^2+0.12*(cos(x-pi))^3+38.8*(cos(x-pi))^4-0.0601*(cos(x-pi))^5
 PERIODIC=NO
... MATHEVAL

# then V1 for T3
MATHEVAL ...
 LABEL=V1_3 ARG=T3 VAR=x
 FUNC=313.9+0.3972*cos(x-pi)-72.12*(cos(x-pi))^2-0.9463*(cos(x-pi))^3+43.87*(cos(x-pi))^4+0.5858*(cos(x-pi))^5
 PERIODIC=NO
... MATHEVAL


# then V2 for T3
MATHEVAL ...
 LABEL=V2_3 ARG=T3 VAR=x
 FUNC=351.9-0.7135*cos(x-pi)-69.01*(cos(x-pi))^2+0.653*(cos(x-pi))^3+47.11*(cos(x-pi))^4+0.41*(cos(x-pi))^5
 PERIODIC=NO
... MATHEVAL



# We can define V0 for T4



MATHEVAL ...
 LABEL=V0_4 ARG=T4 VAR=x
 FUNC=12.16-0.024*cos(x-pi)-43.32*(cos(x-pi))^2+0.12*(cos(x-pi))^3+38.8*(cos(x-pi))^4-0.0601*(cos(x-pi))^5
 PERIODIC=NO
... MATHEVAL

# then V1 for T4
MATHEVAL ...
 LABEL=V1_4 ARG=T4 VAR=x
 FUNC=301.3-0.1478*cos(x-pi)-48.16*(cos(x-pi))^2+0.9948*(cos(x-pi))^3+34.30*(cos(x-pi))^4-1.001*(cos(x-pi))^5
 PERIODIC=NO
... MATHEVAL


# then V2 for T4
MATHEVAL ...
 LABEL=V2_4 ARG=T4 VAR=x
 FUNC=348.8-0.1104*cos(x-pi)-54.71*(cos(x-pi))^2+0.7533*(cos(x-pi))^3+35.14*(cos(x-pi))^4-0.8068*(cos(x-pi))^5
 PERIODIC=NO
... MATHEVAL



# Then you need to build the Hamiltonian for each eletronic state following the FEP combination with lambda parameters. With the ground state and two excited states you will build this Hamiltonian for the torsional potentials describing T1,T2,T3 and T4: 

# This is Vlambda1 for current window
Vlambda1: MATHEVAL ARG=V0_1,V1_1,V2_1,lambda1,lambda2 VAR=x,y,z,l1,l2 FUNC=(1.0-l1)*x+l1*(1-l2)*y+l2*z PERIODIC=NO
Vlambdam1: MATHEVAL ARG=V0_1,V1_1,V2_1,lambda1,lambda2 VAR=x,y,z,l1,l2 FUNC=(1.0-l1+0.04)*x+(l1-0.04)*(1-l2)*y+l2*z PERIODIC=NO
Vlambdap1: MATHEVAL ARG=V0_1,V1_1,V2_1,lambda1,lambda2 VAR=x,y,z,l1,l2 FUNC=(1.0-l1-0.04)*x+(l1+0.04)*(1-l2)*y+l2*z PERIODIC=NO

Vlbias1: BIASVALUE ARG=Vlambda1


# This is Vlambda2 for current window
Vlambda2: MATHEVAL ARG=V0_2,V1_2,V2_2,lambda1,lambda2 VAR=x,y,z,l1,l2 FUNC=(1.0-l1)*x+l1*(1-l2)*y+l2*z PERIODIC=NO
Vlambdam2: MATHEVAL ARG=V0_2,V1_2,V2_2,lambda1,lambda2 VAR=x,y,z,l1,l2 FUNC=(1.0-l1+0.04)*x+(l1-0.04)*(1-l2)*y+l2*z PERIODIC=NO
Vlambdap2: MATHEVAL ARG=V0_2,V1_2,V2_2,lambda1,lambda2 VAR=x,y,z,l1,l2 FUNC=(1.0-l1-0.04)*x+(l1+0.04)*(1-l2)*y+l2*z PERIODIC=NO

Vlbias2: BIASVALUE ARG=Vlambda2


# This is Vlambda3 for current window
Vlambda3: MATHEVAL ARG=V0_3,V1_3,V2_3,lambda1,lambda2 VAR=x,y,z,l1,l2 FUNC=(1.0-l1)*x+l1*(1-l2)*y+l2*z PERIODIC=NO
Vlambdam3: MATHEVAL ARG=V0_3,V1_3,V2_3,lambda1,lambda2 VAR=x,y,z,l1,l2 FUNC=(1.0-l1+0.04)*x+(l1-0.04)*(1-l2)*y+l2*z PERIODIC=NO
Vlambdap3: MATHEVAL ARG=V0_3,V1_3,V2_3,lambda1,lambda2 VAR=x,y,z,l1,l2 FUNC=(1.0-l1-0.04)*x+(l1+0.04)*(1-l2)*y+l2*z PERIODIC=NO

Vlbias3: BIASVALUE ARG=Vlambda3


# This is Vlambda4 for current window
Vlambda4: MATHEVAL ARG=V0_4,V1_4,V2_4,lambda1,lambda2 VAR=x,y,z,l1,l2 FUNC=(1.0-l1)*x+l1*(1-l2)*y+l2*z PERIODIC=NO
Vlambdam4: MATHEVAL ARG=V0_4,V1_4,V2_4,lambda1,lambda2 VAR=x,y,z,l1,l2 FUNC=(1.0-l1+0.04)*x+(l1-0.04)*(1-l2)*y+l2*z PERIODIC=NO
Vlambdap4: MATHEVAL ARG=V0_4,V1_4,V2_4,lambda1,lambda2 VAR=x,y,z,l1,l2 FUNC=(1.0-l1-0.04)*x+(l1+0.04)*(1-l2)*y+l2*z PERIODIC=NO

Vlbias4: BIASVALUE ARG=Vlambda4


#Finally, you can run Parallel Bias metadynamics using the four torsions in the ground and excited states"

PBMETAD ...
ARG=T1,T2,T3,T4 SIGMA=0.2,0.2,0.2,0.2  HEIGHT=1.2 PACE=500 BIASFACTOR=40 LABEL=pb
FILE=HILLS_T1,HILLS_T2,HILLS_T3,HILLS_T4
... PBMETAD

PRINT ARG=T1,T2,T3,T4,Vlambdam1,Vlambda1,Vlambdap1,Vlambdam2,Vlambda2,Vlambdap2,Vlambdam3,Vlambda3,Vlambdap3,Vlambdam4,Vlambda4,Vlambdap4,pb.bias  STRIDE=500 FILE=COLVAR
```
