# Resilience and Disruption in Mexico’s Intermunicipal Mobility Network: A Component Decomposition Approach
#### Erika Cruz-Bonilla<sup>1</sup>, Issa Moussa Diop<sup>2</sup>, Christian Wolff<sup>3</sup>, Hocine Cherifi<sup>4</sup>, and Maribel Hernandez-Rosales<sup>1</sup>
<sup>1</sup> Center for Research and Advanced Studies of IPN, Mexico, 
<sup>2</sup> Universit´e Cote d’Azur, France, 
<sup>3</sup> Mainz University of Applied Sciences,Germany, 
<sup>4</sup> Universit´e De Bourgogne, France.

**Abstract.** Mexico’s intermunicipal mobility network reveals a sharp contrast in the pandemic’s effects. Using 731 daily networks from 2020 to 2021 and a component decomposition approach, the analysis shows
that local components, representing short-distance travel, were heavily disrupted by mobility restrictions, leading to reduced connectivity and smaller community sizes. Meanwhile, global components, reflecting long-distance movement, remained resilient and structurally stable.
These findings highlight how external shocks like COVID-19 disproportionately impact local versus global mobility, revealing the robustness of long-distance networks in times of crisis.

**Keywords:** human mobility, mobile phone data, component structure, COVID-19

# Overview
This program performs network analysis on intermunicipal mobility data. 
It processes daily mobility data (origin-destination pairs) and builds corresponding network graphs.
The program applies community detection algorithms and computes key structural properties, such as local and global components and the k-core of each network.

# Key Functionalities:
- Load daily origin-destination mobility data from CSV files.
- Create NetworkX graph objects to represent the networks for each day.
- Apply the Louvain algorithm to detect communities within the networks.
- Compute local components (intra-community connectivity) and global components (inter-community connectivity).
- Calculate the modularity score to evaluate the strength of the community structure.
- Compute the k-core of the entire network and of individual components.

# Input Format
The program expects CSV files in the ./intermunicipal_od/ directory with the following columns:

- from: Origin node (location ID).
- to: Destination node (location ID).
- count: Number of trips between the locations.
- weight: Weight associated with the trips (could be distance, duration, etc.).
- date: Date of the observation.

# Outputs
- list_g_daily: A dictionary where each key is a date, and the value is a NetworkX graph representing that day's mobility network.
- loc_comps: Local components of the network, representing subgraphs that capture intra-community connections.
- glob_comps: Global components of the network, capturing the connectivity between different communities.
- modularities: Modularity score for each day's network, indicating the strength of its community structure.
- all_communities: Detected communities for each network using the Louvain algorithm.
- lst_k_core: A list of nodes belonging to the k-core of each daily network.

# Functions
**1. local_component(graph, communities)**

Input:

- graph: A NetworkX graph representing the full network.
- communities: A list of lists, where each sublist contains the nodes of a community.

Output:

  - list_community: A list of subgraphs, each representing a local community.
    
**2. global_component(graph, communities)**

Input:

- graph: A NetworkX graph representing the entire network.
- communities: A list of lists, where each sublist contains the nodes of a community.

Output:

- g_community: A list of subgraphs representing global components, i.e., inter-community connections.   

**3. list_k_core_whole_network(list_g_daily)**

Input:

- list_g_daily: A dictionary where each key is a date, and each value is a NetworkX graph for that date.

Output:

- lst_all_core_node: A list of nodes for each daily network belonging to the k-core. 
    
**4. list_k_core_component(components, selected_date=None)**

Input:

- components: A dictionary with dates as keys and lists of subgraphs (components) as values.
- selected_date: (Optional) A list of selected dates for k-core calculation.

Output:

- lst_core: A dictionary where each key is a date, and each value is a list of k-cores for each component.   
    

# Installation
- Install Python 3.x.
- Install the required Python libraries:

  ```
  pip install pandas networkx cdlib
  ```
