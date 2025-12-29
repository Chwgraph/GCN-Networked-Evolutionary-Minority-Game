# Graph Convolution Network Based Analysis For Systematic Performances of Networked Evolutionary Minority Game

# Abstract
 As a classical multi-agent game model, the evolutionary minority game(EMG) has wide applications in financial markets and distributed control systems. The factors that influence the systematic behavior and individual strategy preferences in the networked version of EMG (NEMG) have remained undetermined for a long time. We propose a Graph Convolution Network-based framework to learn a good strategy with a high payoff from the agent's own experience and information shared by its neighbors. Experiments performed on five classes of networks: star graph, Erdos-Renyi random graph, small-world graph, regular graph and complete graph illustrate the effectiveness of this framework and reveal some insights into NEMG settings.

# Method
 We employ Graph Convolutional Networks (GCNs) to learn agent strategies from behavioral data, investigating whether neural networks can capture emergent strategic patterns in networked games. We compare two architectural approaches that differ in their information scope. 

Each graph convolutional layer can be expressed as below:

$$h^{l+1}_{i}=\sigma(\sum_{j \in N(i) \cup \{i\}} \frac{1}{\sqrt{d_i d_j}} W^{(l)} h^{(l)}_{j})$$

where

1. $h^{l}_{i}$: feature vector of node $i$ at layer $l$;
2. $N(i)$: neighbors of node $i$;
3. $d_i, d_j$: degrees of node $i$ and $j$;
4. $W^{(l)}$: learnable weight matrix at layer $l$;
5. $\sigma$: activation function, in our experiments we use $ReLU$;

Full Network GCN: The full network GCN processes the entire graph structure simultaneously. It consists of three graph convolutional layers followed by a fully connected output layer. We use the full network GCN to simulate an agent with global information in the game.

Ego Network GCN: The ego network model processes each agent's local subgraph independently. For the target agent $i$, we extract the ego network which is the induced network of $\{i\} \cup N(i)$, denoted by $G_i$. The architecture uses two convolutional layers followed by a fully connected output layer. One convolutional layer was omitted because less information is needed to handle.

# Experiments
Both GCN models share the same setting in our experiments, not only the training settings, but also the game settings.

## Settings

Input Feature: For each agent, we extract the most recent $h=20$ binary actions, forming the memory vector as feature vectors . 

Target Label: The evolved strategies $s_i$ after evolutionary dynamics serve as ground truth labels.

Loss Function: We use the binary cross-entropy loss.

Optimizer: We use Adam optimizer with learning rate $\alpha=0.001$ trains for 200 epochs. 

Game Settings: We set the memory length $m=4$, selection pressure $ \beta=1.0$, mutation rate $p_{mut}=0.01$ and the number of agents is $N=301$. For bipartite graphs, additionally, we run experiments with $351$ and $501$ agents to see a systematic trend in the change of the attendance number.

## Experiment Framework
We assess learned strategies through simulation-based evaluation. After the training of the full network GCN and ego network GCN, we binarize predicted strategies and initialize a new NMG with the same network topology. By assigning predicted strategies to agents and simulating $20000$ rounds without evolution, we can figure out which strategy performs better by comparing the cumulative average payoff $\overline{P}=\frac{1}{N} \sum_{i=1}^{N} P_i(T)$ where $P_i(T)$ is the cumulative payoff of the agent $i$ after $T$ rounds of games. Note that the cumulative average payoff in fact relies on the attendance number $A$ and can be expressed as $\overline{P}=\min (\frac{A}{N}, \frac{N-A}{N})$, it is always no more than $\frac{N}{2}$. A basic strategy is also applied in the simulations as a comparison reference, which is exactly the evolved strategy setting in basic NEMG we introduced before.


{i\} \cup N(i)$, denoted by $G_i$. The architecture uses two convolutional layers followed by a fully connected output layer. One convolutional layer was omitted because less information is needed to handle.

# Acknowledgements
This work was inspired by a previous work of the author in which variants of the evolutionary mechanism in an Evolutionary Minority Game(EMG) were investigated. Based on it, we studied the networked version by applying machine learning techniques to form this work. For your reference, detailed information about the previous work such as codes and report can be found in the Github repository: https://github.com/Chwgraph/Evolutionary-Minority-Game.

# References
[1] Gian Italo Bischi and Ugo Merlone. Evolutionary minority games with memory. Journal of Evolutionary Economics, 27(5):859–875, 2017. 

[2] Stefano Boccaletti, Vito Latora, Yamir Moreno, Martin Chavez, and D-U Hwang. Complex networks: Structure and dynamics. Physics reports, 424(4-5):175–308, 2006. 

[3] John Adrian Bondy, Uppaluri Siva Ramachandra Murty, et al. Graph theory with applications, volume 290. Macmillan London, 1976. 

[4] Enrique Burgos, Horacio Ceva, and Roberto PJ Perazzo. The evolutionary minority game with local coordination. Physica A: Statistical Mechanics and its Applications, 337(3-4):635–644, 2004. 

[5] Délida Inés Caridi. Properties of interaction networks underlying the minority game. 2014. 

[6] Damien Challet and Y-C Zhang. Emergence of cooperation and organization in an evolutionary game. Physica A: Statistical Mechanics and its Applications, 246(3-4):407–418, 1997. 

[7] Shahar Hod and Ehud Nakar. Evolutionary minority game: The roles of response time and mutation threshold. Physical Review E—Statistical, Nonlinear, and Soft Matter Physics, 69(6):066122, 2004. 

[8] Willemien Kets. The minority game: An economics perspective. arXiv preprint arXiv:0706.4432, 2007. 

[9] Michael Kirley. Evolutionary minority games with small-world interactions. Physica A: Statistical Mechanics and its Applications, 365(2):521–528, 2006. 

[10] Yann LeCun, Bernhard Boser, John S Denker, Donnie Henderson, Richard E Howard, Wayne Hubbard, and Lawrence D Jackel. Backpropagation applied to handwritten zip code recognition. Neural computation,
1(4):541–551, 1989. 

[11] TS Lo, HY Chan, PM Hui, and NF Johnson. Theory of networked minority games based on strategy pattern dynamics. Physical Review E—Statistical, Nonlinear, and Soft Matter Physics, 70(5):056102, 2004.

[12] TS Lo, PM Hui, and NF Johnson. Theory of the evolutionary minority game. Physical Review E, 62(3):4393, 2000. 

[13] Esteban Moro. The minority game: an introductory guide. arXiv preprint cond-mat/0402651, 2004. 

[14 Daehyeon Park, Doojin Ryu, and Robert I Webb. Fear of missing out and market stability: A networked minority game approach. Physica A: Statistical Mechanics and its Applications, 634:129420, 2024. 
[15] Shermila Ranadheera, Setareh Maghsudi, and Ekram Hossain. Minority games with applications to distributed decision making and control in wireless networks. IEEE Wireless Communications, 24(5):184–
192, 2017. 
[16] Lihui Shang and Xiao Fan Wang. Evolutionary minority game on complex networks. Physica A: Statistical Mechanics and its Applications, 377(2):616–624, 2007. 
[17] Steven H Strogatz. Exploring complex networks. nature, 410(6825):268–276, 2001.
[18] Mieko Tanaka-Yamawaki and Seiji Tokuoka. Minority game as a model for the artificial financial markets. In 2006 IEEE International Conference on Evolutionary Computation, pages 2157–2162. IEEE, 2006. 
[19] Si Zhang, Hanghang Tong, Jiejun Xu, and Ross Maciejewski. Graph convolutional networks: a comprehensive review. Computational Social Networks, 6(1):1–23, 2019. 
