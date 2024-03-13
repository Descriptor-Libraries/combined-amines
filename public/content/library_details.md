# Library Details

<div class="centered-container">
     <img src="/amines/content/combined-amines-workflow.png" alt="Combined Amines Workflow" class="responsive-image">
</div>

## Molecule Identification

Molecules from the [primary](https://descriptor-libraries.molssi.org/primary-amines) and [secondary](https://descriptor-libraries.molssi.org/secondary-amines) alkyl amine libraries were combined. These molecules were identified from the Reaxys database, Broad Institute’s Drug Repurposing Hub, and Enamine Building Blocks as described on the respective library pages. 

## Conformational Searching & Conformer Selection

To capture the conformational flexibility of the substrates at a reasonable a computational cost, each secondary alkyl amine was subject to a gas phase molecular mechanics conformational search using Schrödinger MacroModel and the OPLS4 force field.  An ensemble of conformers within 21 kJ/mol (5.02 kcal/mol) of the minimum were collected, excluding mirror-image conformers. 

If the ensemble consisted of greater than 20 conformers, the number of conformers was reduced by atomic root mean square deviation (RMSD)-clustering to the minimum Kelley penalty value and taking the centroids of the resultant clusters. The Kelley index facilitates selection of the optimal number of clusters and ensures the selected conformers structurally diverse.

## DFT Computations

All DFT geometry optimizations and sequent frequency calculations (Gaussian 16, rev C.01) were performed at the B3LYP-D3(BJ)/6-31G(d,p)-LANL2DZ(I, Sn, Se) level of theory. The corresponding geometries were used for a series of single-point energy calculations at the M06-2X/def2-TZVP-SDD(I, Sn, Se) level of theory. 

From the DFT calculations, global, atomic, and bond-level properties were collected for each conformer using a [jupyter notebook](https://github.com/nsf-c-cas/AcidAmine_Descriptor_Predict/tree/main/get_properties_examples). The dynamic range of properties across the conformational ensemble of a single amine was summarized by using five condensed measures for each of the properties.

| Descriptor              | Definition                                                                                      |
| ----------------------- | ------------------------------------------------------------------------------------------------|
| Boltz                   | Boltzmann-weighted average of a property from all the conformers in an ensemble (T = 298.15 K)  |
| max                     | highest value of a property given by any conformer in an ensemble                               |
| min                     | lowest value of a property given by any conformer in an ensemble                                |
| low_E                   | value of a property from the lowest energy conformer in the ensemble                            |
| Boltz_stdev             | Boltzmann-weighted (weighted by mole fraction) standard deviation of a property based on all the conformers in an ensemble (T = 298.15 K) |

Given the similarities between the descriptors collected for primary and secondary alkyl amines, it was feasible to build a combined library with the conserved descriptors and generate the corresponding chemical space representation. In practice, we found that primary and secondary amines populated distinct areas of our projected chemical space representation. For each descriptor supplied to the dimensionality reduction algorithm, we analyzed the distribution of primary and secondary amines. Generally, molecular descriptors had overlap between the two subclasses; however, atom-level descriptors typically had little overlap in descriptor values with the most extreme example being the Boltzmann-average NBO partial charge of N<sup>1</sup>. See the original publication supporting information for more details.

An extended explanation of the computational workflow used to curate the combined primary and secondary alkyl amine library, as well as details on the collected and predicted descriptors can be found in the original publication supporting information.

## Citation
Haas, B. C., Hardy, M. A. Sowndarya S. V., S.; Adams, K.; Coley, C. W.; Paton, R. S.; Sigman, M. S. Rapid Prediction of Conformationally-Dependent DFT-Level Descriptors using Graph Neural Networks for Carboxylic Acids and Alkyl Amines. *ChemRxiv* **2024**. DOI: [10.26434/chemrxiv-2024-m5bpn](https://doi.org/10.26434/chemrxiv-2024-m5bpn)
