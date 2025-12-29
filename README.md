# Graph Convolution Network Based Analysis For Systematic Performances of Networked Evolutionary Minority Game

# Abstract
 As a classical multi-agent game model, the evolutionary minority game(EMG) has wide applications in financial markets and distributed control systems. The factors that influence the systematic behavior and individual strategy preferences in the networked version of EMG (NEMG) have remained undetermined for a long time. We propose a Graph Convolution Network-based framework to learn a good strategy with a high payoff from the agent's own experience and information shared by its neighbors. Experiments performed on five classes of networks: star graph, Erdos-Renyi random graph, small-world graph, regular graph and complete graph illustrate the effectiveness of this framework and reveal some insights into NEMG settings.

# Method
 We employ Graph Convolutional Networks (GCNs) to learn agent strategies from behavioral data, investigating whether neural networks can capture emergent strategic patterns in networked games. We compare two architectural approaches that differ in their information scope. 

Each graph convolutional layer can be expressed as below:

$$h^{l+1}_{i}=\sigma(\sum_{j \in N(i) \cup \{i\}} \frac{1}{\sqrt{d_i d_j}} W^{(l)} h^{(l)}_{j})$$

where

\begin{itemize}
    \item $h^{l}_{i}$: feature vector of node $i$ at layer $l$;
    \item $N(i)$: neighbors of node $i$;
    \item $d_i, d_j$: degrees of node $i$ and $j$;
    \item $W^{(l)}$: learnable weight matrix at layer $l$;
    \item $\sigma$: activation function, in our experiments we use $ReLU$;
\end{itemize}

$\textbf{Full}$ $\textbf{Network}$ $\textbf{GCN}$: The full network GCN processes the entire graph structure simultaneously. It consists of three graph convolutional layers followed by a fully connected output layer. We use the full network GCN to simulate an agent with global information in the game.

# Experiments
Both GCN models share the same setting in our experiments, not only the training settings, but also the game settings.

\subsection{Settings}

\textbf{Input} \textbf{Feature}: For each agent, we extract the most recent $h=20$ binary actions, forming the memory vector as feature vectors $x$. 

\textbf{Target} \textbf{Label}: The evolved strategies $s_i$ after evolutionary dynamics serve as ground truth labels.

\textbf{Loss} \textbf{Function}: We use the binary cross-entropy loss.

\textbf{Optimizer}: We use Adam optimizer with learning rate $\alpha=0.001$ trains for 200 epochs. 

\textbf{Game Settings}: We set the memory length $m=4$, selection pressure $ \beta=1.0$, mutation rate $p_{mut}=0.01$ and the number of agents is $N=301$. For bipartite graphs, additionally, we run experiments with $351$ and $501$ agents to see a systematic trend in the change of the attendance number.

\subsection{Experiment Framework}
We assess learned strategies through simulation-based evaluation. After the training of the full network GCN and ego network GCN, we binarize predicted strategies and initialize a new NMG with the same network topology. By assigning predicted strategies to agents and simulating $20000$ rounds without evolution, we can figure out which strategy performs better by comparing the cumulative average payoff $\overline{P}=\frac{1}{N} \sum_{i=1}^{N} P_i(T)$ where $P_i(T)$ is the cumulative payoff of the agent $i$ after $T$ rounds of games. Note that the cumulative average payoff in fact relies on the attendance number $A$ and can be expressed as $\overline{P}=\min\{\frac{A}{N}, \frac{N-A}{N}\}$, it is always no more than $\frac{N}{2}$. A basic strategy is also applied in the simulations as a comparison reference, which is exactly the evolved strategy setting in basic NEMG we introduced before.


$\textbf{Ego}$ $\textbf{Network}$ $\textbf{GCN}$: The ego network model processes each agent's local subgraph independently. For the target agent $i$, we extract the ego network which is the induced network of $\{i\} \cup N(i)$, denoted by $G_i$. The architecture uses two convolutional layers followed by a fully connected output layer. One convolutional layer was omitted because less information is needed to handle.
