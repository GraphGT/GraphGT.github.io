---
title:  GraphGen
subtitle: A Large-scale Graph Generative Dataset Collection
layout: page
show_sidebar: false
menubar: example_menu
---

<!-- This is another sample page showing how a page can look with a menubar.  -->

## Dataset Categories


## Biomolecules

<!-- Create a data file in the _data directory and use the following format (if using yml) -->
### QM9 

**Description**

It is an enumeration of around 134k stable organic molecules with up to 9 heavy atoms (carbon, oxygen, nitrogen and fluorine). As no filtering is applied, the molecules in this dataset only reflect basic structural constraints.

**Acknowledgements**

R. Ramakrishnan, P. O. Dral, M. Rupp, and O. A. Von Lilienfeld, “Quantum chemistry structures and properties of 134 kilo molecules,” Scientific data, vol. 1, no. 1, pp. 1–7, 2014.

---

### ZINC 

**Description**

This dataset is a curated set of 250k commercially available drug-like chemical compounds. On average, these molecules are bigger (about 23 heavy atoms) and structurally more complex than the molecules in QM9.

**Acknowledgements**

J. J. Irwin, T. Sterling, M. M. Mysinger, E. S. Bolstad, and R. G. Coleman, “Zinc: a free tool to discover chemistry for biology,” Journal of chemical information and modeling, vol. 52, no. 7, pp. 1757–1768, 2012.

---

### MOSES

**Description**

Molecular Sets (MOSES) is a benchmark platform for distribution learning based molecule generation. Within this benchmark, MOSES provides a cleaned dataset of molecules that are ideal of optimization. It is processed from the ZINC Clean Leads dataset.

**Acknowledgements**

Polykovskiy, Daniil, et al. "Molecular sets (MOSES): a benchmarking platform for molecular generation models." Frontiers in pharmacology 11 (2020).

---

### ChEMBL

**Description**

ChEMBL is a manually curated database of bioactive molecules with drug-like properties. It brings together chemical, bioactivity and genomic data to aid the translation of genomic information into effective new drugs.

**Acknowledgements**

Mendez, David, et al. “ChEMBL: towards direct deposition of bioassay data.” Nucleic acids research 47.D1 (2019): D930-D940.

---

### CEPDB 

**Description**

This dataset consists of organic molecules with an emphasis on photo-voltaic applications. The con- tained molecules have 28 heavy atoms on average and contain six to seven rings each.

**Acknowledgements**

J.Hachmann,R.Olivares-Amaya,S.Atahan-Evrenk,C.Amador- Bedolla, R. S. Sa ́nchez-Carrera, A. Gold-Parker, L. Vogt, A. M. Brockway, and A. Aspuru-Guzik, “The harvard clean energy project: large-scale computational screening and design of or- ganic photovoltaics on the world community grid,” The Journal of Physical Chemistry Letters, vol. 2, no. 17, pp. 2241–2251, 2011.

---

### Protein

**Description**

This dataset contains 918 protein graphs with 100 ≤ \|V\| ≤ 500. Each protein is represented by a graph, where nodes are amino acids and two nodes are connected if they are less than 6 Angstroms apart.

**Acknowledgements**

P. D. Dobson and A. J. Doig, “Distinguishing enzyme structures from non-enzymes without alignments,” Journal of molecular biol- ogy, vol. 330, no. 4, pp. 771–783, 2003.

---

### Enzymes 

**Description**

This dataset contains protein tertiary structures representing 600 enzymes. Nodes in a graph (pro- tein) represent secondary structure elements, and two nodes are connected if the corresponding elements are interacting. The node labels indicate the type of secondary structure, which is either helices, turns, or sheets.

**Acknowledgements**

I. Schomburg, A. Chang, C. Ebeling, M. Gremse, C. Heldt, G. Huhn, and D. Schomburg, “Brenda, the enzyme database: updates and major new developments,” Nucleic acids research, vol. 32, no. suppl 1, pp. D431–D433, 2004.

---

### Brain Networks

**Will be released soon**

---

### Molecule Optimization

**Problem Background**

The goal of drug discovery is to design molecules with desirable chemical properties. The task is challenging since the chemical space is vast and often difficult to navigate. One of the prevailing approaches, known as matched molecular pair analysis (MMPA), learns rules for generating “molecular paraphrases” that are likely to improve target chemical properties. The setup is analogous to machine translation: MMPA takes as input molecular pairs f(X; Y )g, where Y is a paraphrase of X with better chemical properties. However, current MMPA methods distill the matched pairs into graph transformation rules rather than treating it as a general translation problem over graphs based on parallel data. Molecular optimization can be formalized as graph-to-graph translation. Given a corpus of molecular pairs, the goal is to learn to translate input molecular graphs into better graphs.

**Data Collection**

Following standard practice in MMPA, we construct training sets by sampling molecular pairs (X; Y ) with significant property improvement and molecular similarity sim(X; Y ). The similarity constraint is also enforced at evaluation time to exclude arbitrary mappings that completely ignore the input X. We measure the molecular similarity by computing Tanimoto similarity over Morgan fingerprints (Rogers & Hahn, 2010). Next we describe how these tasks are constructed.

**Dataset Decription**

Penalized logP The goal is to improve the penalized logP score of molecules under the similarity constraint. We experiment with two similarity constraints(0.4 and 0.6), and we extracted 99K and 79K translation pairs respectively from the ZINC dataset for training.

Drug likeness (QED) This task is to improve drug likeness of compounds. Specifically, the model needs to translate molecules with QED scores (Bickerton et al., 2012) within the range (0.7-0.8) into the higher range (0.9-1.0). This task is challenging as the target range contains only the top 6.6% of molecules in the ZINC dataset. We extracted a training set of 88K molecule pairs with similarity constraint (0.4). The test set contains 800 molecules.

Dopamine Receptor (DRD2) This task is to improve a molecule’s biological activity against a biological target named the dopamine type 2 receptor (DRD2). We use a trained model from Olivecrona et al. (2017) to assess the probability that a compound is active. We ask the model to translate molecules with predicted probability p < 0:05 into active compounds with p > 0.5. The active compounds represent only 1.9% of the dataset. With similarity constraint 0.4, we derived a training set of 34K molecular pairs from ZINC. The test set contains 1000 molecules.

**Acknowledgements**

Jin, W., Yang, K., Barzilay, R., & Jaakkola, T. (2018). Learning multimodal graph-to-graph translation for molecular optimization. arXiv preprint arXiv:1812.01070.

---

### Chemical Reaction

**Problem Background**

Reaction prediction remains one of the major challenges for organic chemistry and is a prerequisite for efficient synthetic planning. It is desirable to develop algorithms that, like humans, “learn” from being exposed to examples of the application of the rules of organic chemistry.

**Data Collection**

The chemistry preaction product prediction can be formalized as the graph translation problem, thus predicting the product (target graph) of chemical reaction given the reactant (input graph). Each molecular graph consists of atoms as nodes and bond as edges. The input molecule graph has multiple connected components since there are multiple molecules comprising the reactants. The reactions used for training are atom-mapped so that each atom in the product graph has a unique corresponding atom in the reactants. We collected reactions from USPTO granted patents (Lowe, 2014). we obtained a set of 5,000 reactions (reactant-product pair). Atom (node) features include its elemental identity, degree of connectivity, number of attached hydrogen atoms, implicit valence, and aromaticity. Bond (edge) features include bond type (single, double, triple, or aromatic), and whether it is connected.

**Description**

There are totally 7180 pairs of reactant anf product molecule graph in the dataset. The number of nodes (atoms) of molecule ranges from 9 to 20, and the number of atoms for each pair is recorded and stored in the file "Num_nodes.cxv". The file folder "mol_edge" store all the adjacent matrix for the input and target graph. The dimension of the adjacent matrix is 20 by 20, and for those graphs whose nodes are less than 20, we use zero to pad. The values in adjacent matrix is in [0,1,2,3,4] representing five bond types (none, single, double, triple, or aromatic). The folder "Mol_nodes" stores the node features for all the nodes in each graph. The node feature indicates the atom type (82 types) which are embedded by one-hot vector with 82 dimensions. In this problem setting, the node feature remains unchanged during the translation.

[Mol_edge](https://exchangelabsgmu-my.sharepoint.com/:u:/g/personal/xguo7_masonlive_gmu_edu/EZzBXqVYGQZBijWzB6XV-k4BYrQjJp4J2GKDPlhYdDfkqw)

[Mol_nodes](https://exchangelabsgmu-my.sharepoint.com/:u:/g/personal/xguo7_masonlive_gmu_edu/EWPhBYlZ8x1Ptn5esMqaKOABa11TAt_7UJrYmSGHBowpBg)

[Num_nodes](https://exchangelabsgmu-my.sharepoint.com/:x:/g/personal/xguo7_masonlive_gmu_edu/EVLlh7btdvxPgsZaym_TyA4BQnyqE_oNE_jfEtM2v1gbTA)

More datasets of chemical reaction can be found in [USPTO-15K](https://github.com/wengong-jin/nips17-rexgen).

Acknowledgements

Guo X, Zhao L, Nowzari C, Rafatirad S, Homayoun H, Dinakarrao SM. Deep Multi-attributed Graph Translation with Node-Edge Co-evolution. Inhe 19th International Conference on Data Mining (ICDM 2019), pp. to appear 2019.

D. Lowe, “Patent reaction extraction: downloads,” 2014.

---

## [Physical Simulation Networks](#physics)

### N-body Simulations

Name | Type | Samples| Nodes | Edges | Description
------------ | ------------- | ------------ | ------------ | ------------ | ------------ |
N-body | Content from cell 2
Content in the first column | Content in the second column

---

## Collaboration Networks

### Citation Networks 

**Description**

Cora and Citeseer are citation networks; nodes correspond to publications and an edge represents one paper citing the other. Node labels represent the publication area. The Cora dataset contains 2708 nodes, 5429 edges, 7 classes and 1433 features per node. The Cite- seer dataset contains 3327 nodes, 4732 edges, 6 classes and 3703 features per node

---

### Co-authorship Networks 



---

## Circuit Networks

**Data Collection**

In circuit simplification, a logical expression is reduced to a logically equivalent expression with fewer operations. We construct a dataset of random circuits with 15-30 nodes (3-8 variables). Each node in the graph corresponds to one of four node types: variables, NOT-gates, OR-gates, and AND-gates. Node features are given by a one-hot encoding of the four node types. All generated circuits were valid, i.e. they have a single sink node, NOT-gate nodes have a single input, variable nodes have no inputs, and OR and AND-gate nodes have at least two inputs. To produce ground truth simplifications, the generated logical expressions corresponding to each graphs were simplified using the Sympy Python library, which provides an equivalent expression either in conjunctive normal form (CNF) or disjunctive normal form (DNF), depending on which is more compact. Any circuits that simplified to True (tautology) or False (unsatisfiable) were excluded. We use 10,000 circuit pairs for training and 2,500 pairs for testing. Node features are given by a one-hot encoding of the four node types. [Circuit dataset] (https://github.com/claradepaolis/D2DRNN)

**Acknowledgements**

Kaluza, M. C. D. P., Amizadeh, S., & Yu, R. A Neural Framework for Learning DAG to DAG Translation.

---

## Traffic Networks

Traffice Networks 

---

### Authetication Networks

**Problem Background**

Important trade secrets stored in an enterprise’s computer network are extremely hard to defend from theft-of-trade-secret behaviors, which involve highly sophisticated activities in terms of malicious authentication paths over cyber-networks. Malicious detection involves learning from rich historical attack examples, which however are not available for all the employee accounts. The generic distribution of theft behaviors from historical attacks on some accounts can be learned and used to synthesize a range of possible malicious authentication graphs for other accounts based on their regular authentication graphs.

**Contents**

The goal of this application was to forecast future potential users' malicious authentication graphs given the user’s normal authentication graph, which is an one-to-many mapping version of graph translation. This dataset includes the authentication activities of 97 users on their accessible computers and servers in an enterprise computer network (Kent, 2015). Each user account generates a log file recording the computer accessing history, which could be formulated as a directed weighted graph called authentication graph, where nodes represent computers and the directed edges weights represent the authentication activities with certain frequencies. This data set spans one calendar year of contiguous activity spanning 2012 and 2013. It originated from 33.9 billion raw event logs (1.4 terabytes compressed) collected across the LANL enterprise network of approximately 24,000 computers. The input graphs represent authentication events collected from individualWindows-based desktop computers, servers, and Active Directory servers. The target graphs present specific events taken from the authentication data that present known red team compromise events, as we call malicious event. The red team data can used as ground truth of bad behavior which is different from normal user. Each graph can represent the log-on activity of one user in a time window. This task is the one-many-mapping, which means for each input graph, there can be many potential target graphs that follows the same distribution.

**Description**

There are two subsets of different sizes of graphs (i.e., 50 and 300). For each subset, we have train anf test folder seperately. Train set contains the graph pairs (one-to-one) which are just used for training. Test set contains data for each user. For each user, there are several input graphs (i.e. regular user authentication activity graph) and several target graphs (i.e. malware user authentication acticity graph). There input and target graphs in test set are not one-to-one, which can be tested by indirect evaluation. There is no node attributes for this dataset, and only edge attribute is considered. For each graph, the value of i(th) row and j(th) colomn refers to the edge attribute of Node i and j (0 refers to no links).

[Auth_50](https://exchangelabsgmu-my.sharepoint.com/:u:/g/personal/xguo7_masonlive_gmu_edu/Ed5FSLojkadImn4PvDgln_8B6pCP0oePBXbq-osyDpBcFQ)

[Auth_300](https://exchangelabsgmu-my.sharepoint.com/:u:/g/personal/xguo7_masonlive_gmu_edu/EbEM8KApJhlAuReZTsgzBjkBv4zVYpKOtLuE7ZK0J46q-w)

**Acknowledgements**

Guo, X., Wu, L., & Zhao, L. (2018). Deep graph translation. arXiv preprint arXiv:1805.09980.

---

### IoT Networks

**Problem Background**

The process of malware confinement over IoT (Internet of Things) is typically a graph translation problem. A device infected in an IoT network can propagate to other nodes connected to it, leading to contaminating the whole network, such as MiraiBot attack. As such, it is non-trivial to confine the malware to limit the infection and also equally important to maintain overall network connectivity and performance. The malware confinement takes the initial status of IoT as input, and predicts the target graph which is ideally the optimal status of the network with modified connections (i.e., edges) and devices (i.e., nodes) state that helps to limit malware propagation and maintain network throughput. Tranditional malware confinement are based on ad-hoc methods, which heavily rely on intensive handcrafting and domain-specific mechanistic models that could be extremely time- and resource- consuming to run in large scale. Hence, a generic, efficient, and end-to-end method is in demand, which is able to comprehensively learn the translation mapping, remedy human bias by enjoying the large historical data, and achieve efficient prediction.

**Dataset Collection**

Malware dataset are collected for malware confinement prediction. There are three sets of IoT nodes at different amount (20, 40 and 60) encompassing temperature sensors connected with Intel ATLASEDGE Board and Beagle Boards (BeagleBone Blue), communicating via Bluetooth protocol. Benign and malware activities are executed on these devices to generate the initial attacked networks as the input graphs. Benign activities include MiBench [34] and SPEC2006 [35], Linux system programs, and word processor. The nodes represent devices and node attribute is a binary value referring to whether the device is compromised or not. Edge represents the connection of two devices and the edge attribute is a continuous value reflecting the distance of two devices. The real target graphs are generated by the classical malware confinement methods: stochastic controlling with malware detection. We collected 334 pairs of input and target graphs with different contextual parameters (infection rate, recovery rate, and decay rate) for each of the three datasets. In this dataset, there are both nodes attributes and edge attributes considered.

**Description**

There are three subsets with different graph sizes. Each input/target graph is stored in the file with name " IoT-[graph_size]-[input/output]-[infection rate]-[recovery rate]-[decay rate]-[index].csv". The infection rate, recovery rate and decay rate can be used as the contextual controlling parameters in generating the target graph. The value of i(th) row and j(th) colomn refers to the phsical distance of Node i and j (0 refers to no links). The value of i(th) row and i(th) colomn refers to the node attribute (i.e. device status) of the Node i.

[IoT_20](https://exchangelabsgmu-my.sharepoint.com/:u:/g/personal/xguo7_masonlive_gmu_edu/EcZsWKkLcxBKpaZ-X7_CHcoB5VAEzd9AGYgxATWIUPAsRw)

[IoT_40](https://exchangelabsgmu-my.sharepoint.com/:u:/g/personal/xguo7_masonlive_gmu_edu/Eekr5lVPZBlMk6_1KkBgZbIBWPRYzDrA6tt9WOhJ1yUbEA)

[IoT_60](https://exchangelabsgmu-my.sharepoint.com/:u:/g/personal/xguo7_masonlive_gmu_edu/EY6Emi5mPQdDodCY0dK_ISQB4oYGpRnaMfxY2EpSCE7VLw)

Acknowledgements

Guo X, Zhao L, Nowzari C, Rafatirad S, Homayoun H, Dinakarrao SM. Deep Multi-attributed Graph Translation with Node-Edge Co-evolution. In the 19th International Conference on Data Mining (ICDM 2019), pp. to appear 2019.

---

### Skeleton Graphs

Human Skeleton Point Clouds 

---

### Scene Graphs

**Description**

CLEVR provides a dataset for visual question answer, which can be formalized as a spatial-graph dataset. There are $10$ objects in the image with different 3D locations. Each  object is identified by its shape, such as sphere, cylinder, and cube. The relationship between two objects can be categorized into four types: right, behind, front, left, with directions. Thus, each image can be formalized as a labeled directed graph with different edge types and node types. Thus, the spatial information of each nodes is closely correlated with the edge types between each pair of nodes. There are 70,000 training samples and 15,000 testing samples.

**Acknowlegements**

Johnson, Justin and Hariharan, Bharath and van der Maaten, Laurens and Fei-Fei, Li and Lawrence Zitnick, C. and Girshick, Ross. CLEVR: A Diagnostic Dataset for Compositional Language and Elementary Visual Reasoning. In the Proceedings of the IEEE Conference on Computer Vision and Pattern Recognition (CVPR) 2017.

---

## Synthetic Graphs
---
### Scale-free Graphs

This dataset fits the "one-to-many" mapping graph translation version. There are no node features in the dataset, and the goal is to learn the mapping from the input graphs' topology to the target graph's topology. Each input graph is generated as a directed scalefree network, which is a network whose degree distribution follows power-law property (Bollobas´ et al., 2003). To generate a target graph, a node will by selected as target node with probability proportional to its in-degree, which will be linked to a new source node with probability of 0.41. Similarly, a node will by selected as source node with probability proportional to its out-degree, which will be linked to a new target node with probability of 0.54. Then, a corresponding target graph is generated by adding m (m equals the number of nodes of the input graph) edges between two nodes. Thus, both input and target graphs are directed scale-free graphs.

**Content**

There are five subsets of data with different graph size (i.e. number of nodes): 10, 20, 50, 100, and 150. In each subset, each input and output graph are stored in the "scale-(graph_size)-input-index.csv" and "scale-(graph_size)-target-index.csv" file. For each file, the value in i(th) comlume, j(th) row indicates whether the number of connections (edge weights) between Node i and Node j (1 indicating there is an edge and 0 otherwise). These dataset can be downloaded through the following links:

[Scale_free_150](https://exchangelabsgmu-my.sharepoint.com/:u:/g/personal/xguo7_masonlive_gmu_edu/EQ7FRL8QWYdPg25QaCe0VpEBHwioyA4nEjP2GDgiVQQwVw)

[scale_free_100](https://exchangelabsgmu-my.sharepoint.com/:u:/g/personal/xguo7_masonlive_gmu_edu/EXLsRjyz7z1HhRur-F9jkpwBFfRhO14NfQxXoLSHwCzYfg)

[scale_free_50](https://exchangelabsgmu-my.sharepoint.com/:u:/g/personal/xguo7_masonlive_gmu_edu/Ec7OxxtCrW5Nr7itfQAlcagBQaRNG-ttRt-DZkj8jBxphQ)

[scale_free_20](https://exchangelabsgmu-my.sharepoint.com/:u:/g/personal/xguo7_masonlive_gmu_edu/EQ3WsWoTBwNLsQXQOIwChOgBsbDIUfZpp0tmvJYGp0JrtA)

[scale_free_10](https://exchangelabsgmu-my.sharepoint.com/:u:/g/personal/xguo7_masonlive_gmu_edu/EartEwo94NtJrsBUSDCaSyIBYgHxLSVj6qwziixaQHHHdw)

**Acknowledgements**

Guo, X., Wu, L., & Zhao, L. (2018). Deep graph translation. arXiv preprint arXiv:1805.09980.

---

### Erdos-Renyi Graphs

This dataset fit the problem of "one-to-one" mapping verision of graph translation. For each pair of graphs, the input graph is generated by the Erdos Renyi model with the edge probability of 0.2. The target graph topology is the 2-hop connection of the input graph, where each edge in the target graph refers to the 2-hop reachability in the input graph (e.g. if node i is 2-hop reachable to node j in the input graph, then they are connected in the target graph). There are edge and node attributes for graphs in this dataset: the edge attributes E_(i,j) denotes the existence of the edge and the node attributes are continuous values computed following the polynomial function: f(x) : y = ax^2 + bx + c(a =0; b =1; c= 5), where x is the node degree and f(x) is the node attribute.

**Contents**

There are three subsets of data with different graph size (i.e. number of nodes): 20, 40, and 60. In each subset, each input and output graph are stored in the "ER-(graph_size)-input-index.csv" and "ER-(graph_size)-target-index.csv" file. For each file, the value in i(th) comlume, j(th) row indicates whether the number of connections (edge weights) between Node i and Node j (1 indicating there is an edge and 0 otherwise). The value in i(th) row and i(th) column indicates the node attributes of the i(th) node. These dataset can be downloaded through the following links:

[ER_20](https://exchangelabsgmu-my.sharepoint.com/:u:/g/personal/xguo7_masonlive_gmu_edu/EacBEmToBKdPtOhjJocARikBV6WRr7kNs50QyFShsx1k1w)

[ER_40](https://exchangelabsgmu-my.sharepoint.com/:u:/g/personal/xguo7_masonlive_gmu_edu/EU7TdmWC_z1HvY3KLcPonZwBB167_MYTQZuW8wSso4Qc1g)

[ER_60](https://exchangelabsgmu-my.sharepoint.com/:u:/g/personal/xguo7_masonlive_gmu_edu/EQYmsg6wu3ZAuvHS1Klc_gwBdZP3jCl_PM2p6p7nLMZ66g)

**Acknowledgements**

Guo X, Zhao L, Nowzari C, Rafatirad S, Homayoun H, Dinakarrao SM. Deep Multi-attributed Graph Translation with Node-Edge Co-evolution. Inhe 19th International Conference on Data Mining (ICDM 2019), pp. to appear 2019.

---

### Barab´asi-Albert Graphs

This dataset fit the problem of "one-to-one" mapping verision of graph translation. For each pair of graphs, the input graph is generated by the Barab´asi-Albert model. The target graph topology is the 2-hop connection of the input graph, where each edge in the target graph refers to the 3-hop reachability in the input graph (e.g. if node i is 3-hop reachable to node j in the input graph, then they are connected in the target graph). There are edge and node attributes for graphs in this dataset: the edge attributes E_(i,j) denotes the existence of the edge and the node attributes are continuous values computed following the polynomial function: f(x) : y = ax^2 + bx + c(a =0; b =1; c= 5), where x is the node degree and f(x) is the node attribute.

**Contents**

There are three subsets of data with different graph size (i.e. number of nodes): 20, 40, and 60. In each subset, each input and output graph are stored in the "BA-(graph_size)-input-index.csv" and "BA-(graph_size)-target-index.csv" file. For each file, the value in i(th) comlume, j(th) row indicates whether the number of connections (edge weights) between Node i and Node j (1 indicating there is an edge and 0 otherwise). The value in i(th) row and i(th) column indicates the node attributes of the i(th) node. These dataset can be downloaded through the following links:

[BA_20](https://exchangelabsgmu-my.sharepoint.com/:u:/g/personal/xguo7_masonlive_gmu_edu/ESU5immRQ3xCvxkAy0LFvlgBTJrF0eHDosjRhnnayUXqHw)

[BA_40](https://exchangelabsgmu-my.sharepoint.com/:u:/g/personal/xguo7_masonlive_gmu_edu/EaihwXZdW2dHpl0X22dtD5wBcKFD9X6F1SoYhDKzAhRX1w)

[BA_60](https://exchangelabsgmu-my.sharepoint.com/:u:/g/personal/xguo7_masonlive_gmu_edu/EV96-W8Kw1hFnMxDudDWCk0BK6J24_my2yD7KrgJLR-yWw)

**Acknowledgements**

Guo X, Zhao L, Nowzari C, Rafatirad S, Homayoun H, Dinakarrao SM. Deep Multi-attributed Graph Translation with Node-Edge Co-evolution. Inhe 19th International Conference on Data Mining (ICDM 2019), pp. to appear 2019.



<!-- ```yml
- label: Example Menu
  items:
    - name: Home
      link: /
    - name: Pages
      link: #
      items:
        - name: Page With Sidebar 
          link: /page-1/
        - name: Page Without Sidebar
          link: /page-2/
        - name: Page With Menubar
          link: /page-3/
    - name: Blog
      link: /blog/
``` -->

<!-- ### Multiple menus

You may make multiple menus in the same file, separated by the label

```yml
- label: Menu Label
  items:
    - name: Example item
      link: /example-item/
- label: Second Menu Label
  items:
    - name: Parent Item
      link: /parent-item/
      items:
        - name: Sublink 
          link: /sublink/
        - name: Sublink 2
          link: /sublink2/
- label: Third Menu Label
  items:
    - name: Another example item
      link: /another-example-item/
``` -->
