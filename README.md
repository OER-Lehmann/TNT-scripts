# TNT-scripts

General-purpose TNT scripts for everyone to use.

- [Tree Testing Under Implied Weights](#tree-testing-under-implied-weights-ttuiwrun).

## Tree Testing Under Implied Weights (`ttuiw.run`)

The script `ttuiw.run` provides a small Windows interface to carry out sensitivity analyses using equal weights and implied weights with several values of the concavity constant *k*. It only works for Windows OS. Any version capable of running TNT should work.

### A brief user guide

#### Using `ttuiw.run`

To run `ttuiw.run` you must:
1. Download `ttuiw.run` from this repository and place it in TNT's folder.
2. Run the graphical interface of TNT (`tnt.exe`, the one with the light-blue tetrahedron logo). The script won't work from the stand-alone command line (`tntline.exe`).
3. Load your phylogenetic matrix.
4. Type `run ttuiw.run;` in the field that reads "Enter command:" at the bottom of the window and press Enter. This should open `ttuiw.run` window. If you can't find the "Enter command:" field, go to File and select Command Line.
5. Select the desired options.
6. Press "OK".

Below there is a detailed description of the available options and of the outputs of the script.

#### k-values to explore frame

This frame allows the selection of the values of the concavity constant *k* to explore, as well as the inclution of an equal weights analysis. The "From" spinbox selects the starting value. A value of 0 indicates a first round of analysis with equal weights. The "By" spinbox selects the increment in the value of *k*. The "To" spinbox selects the highest value of *k* that is to be explored.

Some examples:
- If *From* is set to 0, *By* is set to 1, and *To* is set to 20 a total of 21 analyses will be carried out: one with equal weights and twenty with implied weighting, with *k* equal to 1, 2, 3, ..., 18, 19, and 20.
- If *From* is set to 0, *By* is set to 2, and *To* is set to 100 a total of 51 analyses will be carried out: one with equal weights and fifty with implied weighting, with *k* equal to 2, 4, 6, ..., 96, 98, and 100.
- If *From* is set to 1, *By* is set to 1, and *To* is set to 10 a total of 10 analyses will be carried out: ten analyses with implied weighting, with *k* equal to 1, 2, 3, ..., 8, 9, and 10.

Note that  *k* can only take integer values in this implementation.

#### Comparisons frame

This frame allows the selection of some options to quickly compare the output of the the analyses under different values of *k*.

- Robinson-Foulds dist.: Calculate the Robinson-Foulds distance between the unique trees obtained throughout all analyses.
- Equal trees: Show which analyses resulted in identical trees.

#### Select search frame

This frame allows the selection of the tree exploration strategy. All of them start with the use of traditional or new technologies and after them they perform a round of TBR with the resulting trees.


- Soft traditional: Equivalent to the command `mult = repl 50 tbr hold 3; bb = tbr;`.
- Normal traditional: Equivalent to the command `mult = repl 100 tbr hold 3; bb = tbr;`.
- Normal traditional + ratchet: Equivalent to the command `mult = repl 100 tbr hold 3; rat = iter 50 nums 2; bb = tbr;`.
- Default new techs, 3 hits: Equivalent to the command `xmult = hits 3; bb = tbr;`.
- Default new techs + drift, 5 hits: Equivalent to the command `xmult = hits 5 drift 10 hold 2; bb = tbr;`.
- Default new techs + more drift, 10 hits: Equivalent to the command `xmult = hits 10 drift 20 hold 2; bb = tbr;`.

#### Outputs

The script *always* creates a file called `ttuiw_output.tre` in the same folder where it is located. This file contains the strict consensus of the trees obtained from each analysis, in order. You should be carefully identify each tree, following the parameters you set in the k-values to explore frame. Also, the file will be overwritten if you run the script again, so be mindful and rename it and/or move it to another folder before running `ttuiw.run` again.

If the option equal trees was selected, a grid will be displayed on the TNT window, showing which trees are identical between analyses. A bit of caution should be taken here, as a comparison between strict consensus trees is ill-advised as different sets of trees can produce the same strict consensus tree. This is shouldn't be a common problem as *most* matrices produce a single most parsimonious tree when analysed with implied weighting (personal observation), and thus the strict consensus is identical to the most parsimonious tree.

If the option Robinson-Foulds dist. is selected, a grid showing the Robinson-Foulds distance between the unique trees found through the analyses. Note that a file named `ttuiw_output2.tre` will be created. It will contain only the unique trees obtained through all analyses. For example, if all analyses yielded the same tree only one tree will be present in it. Else, the unique trees will be orderder as they appear in the analyses, which can be seen in the output of eqaul trees on the TNT window.

### Use history

`ttuiw.run` has been used so far in 7 publications:
1. Viglino, M., Buono, M.R., Gutstein, C.S., Cozzuol, M.A., and Cuitiño, J.I. 2018. A new dolphin from the early Miocene of Patagonia, Argentina: Insights into the evolution of Platanistoidea in the Southern Hemisphere. *Acta Palaeontologica Polonica* **63**(2): 261-277. DOI: [10.4202/app.00441.201](https://doi.org/10.4202/app.00441.201).
2. Alvarez, M.J. 2019. Phylogenetic analysis of the genus *Retrotapes* del Río, 1997 (Bivalvia, Veneridae) and systematic analysis of its taxa from Chile. *Journal of Paleontology* **93**(4): 685-701. DOI: [10.1017/jpa.2018.110](https://doi.org/10.1017/jpa.2018.110). [Not mentioned in Acknowledgements, must be confirmed].
3. Pérez, D.E. 2019. Phylogenetic relationships of the family Carditidae (Bivalvia: Archiheterodonta). *Journal of Systematic Palaeontology* **17**(16): 1359-1395. DOI: [10.1080/14772019.2018.1532463](https://doi.org/10.1080/14772019.2018.1532463).
4. Viglino, M., Buono, M.R., Fordyce, R.E., Cuitiño, J.I., and Fitzgerald, E.M.G. 2019. Anatomy and phylogeny of the large shark-toothed dolphin *Phoberodon arctirostris* Cabrera, 1926 (Cetacea: Odontoceti) from the early Miocene of Patagonia (Argentina). *Zoological Journal of the Linnean Society* **185**(2):511-542. DOI: [10.1093/zoolinnean/zly053](https://doi.org/10.1093/zoolinnean/zly053).
5. Alvarez, M.J., and del Río, C.J. 2020. Phylogeny of the Eocene Antarctic Tapetinae Gray, 1851 (Bivalvia, Veneridae) from the La Meseta and Submeseta formations. *Journal of Paleontology* **94**(5): 799-818. DOI: [10.1017/jpa.2020.30](https://doi.org/10.1017/jpa.2020.30).
6. Pérez, D.E., and Giachetti, L.M. 2020. Is *Cyclocardia* (Conrad) a wastebasket taxon? Exploring the phylogeny of the most diverse genes of the carditidae (Archiheterodonta, Bivalvia). *Palaeontology* **63**(3):477-495. DOI: [10.1111/pala.12467](https://doi.org/10.1111/pala.12467).
7. Viglino, M., Gaetán C.M., Cuitiño, J.I., and Buono M.R. 2021. First toothless platanistoid from the early Miocene of Patagonia: the golden age of diversification of the Odontoceti. *Journal of Mammalian Evolution* **28**:337-358. DOI: [10.1007/s10914-020-09505-w](https://doi.org/10.1007/s10914-020-09505-w).
