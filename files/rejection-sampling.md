### Rejection sampling


We want to sample a network of $N$ nodes from a probability distribution given by $P(A_{ij}=1) = \frac{\exp(f(i,j))}{1 + \exp(f(i,j))}$ where $f(i,j)$ is a real-valued function, and $A_{ij}$ is the adjacency matrix. Sampling a network from $P$ is computationally expensive since there are roughly $N^2$ number of node pairs for which to decide whether to place an edge ($A_{ij}=1$) or not ($A_{ij}=0$). We propose the rejection sampling to circumvent the expensive complexity.

The rejection sampling consists of the following steps:
1. Sample a network with another probability distribution $Q$, referred to as the *proposed* distribution. The sampled network has more edges than that generated from $P$.
2. For each edge $(i,j)$ generated from $Q$, we keep the edge with an acceptance probability $R(i,j)$ or discard it with probability $1-R(i,j)$.
The proposed distribution $Q$ is defined such that $P(A_{ij}=1) \leq Q(A_{ij}=1)$ and the acceptance probability is defined such that $R(i,j)\cdot Q(A_{ij}=1)=P(A_{ij}=1)\quad\text{or}\quad R(i,j) = \frac{P(A_{ij}=1)}{Q(A_{ij}=1)}.$
In other words, we generate a denser network using $Q$ and discard some edges such that the final network matches with that generated from $P$.

The rejection sampling is equivalent to the original brute-force approach if $Q(i,j)=1$. In this case, $Q$ generated a fully-connected network, and the edges are accepted with probability $R(i,j)$. There are roughly $N^2$ number of edges to decide whether to accept or not (the second step). Thus, the computation cost remains the same ( ${\cal }$ ${\cal O}(N^2)$ ).

The rejection sampling is more efficient when $Q$ generates a network sparser than a fully connected network. In fact, if $Q$ generates a network with $M_q$ edges, we have a cost $C_q$ for generating the network and an additional cost of checking those $M_q$ edges, resulting in the computational complexity of $O(C_q + M_q)$.


The key to this approach is the choice of $Q$, which should be (1) computationally efficient and (2) as close to $P$ as possible, and (3) $P(A_{ij}=1) \leq Q(A_{ij}=1)$ for all pairs of nodes. We use
$Q(A_{ij}=1) = \exp(f(i,j)).$
It is easy to verify $P < Q$ since $1 + \exp(f(i,j))$—the denominator of $P$—is greater than 1. The acceptance probability, thus, is given by
$R(i,j) = \frac{1}{1 + \exp(f(i,j))}$
# Configuration model

Let us consider a specific model to showcase the idea. The configuration model corresponds to
$f(i,j) = -\alpha_i - \alpha_j,$
where $\alpha_i$ is the parameter for node $i$ that controls its degree. Now, the proposed distribution is then given by
$Q(i,j) = \exp(\alpha_i)\exp(\alpha_j).$
Note that $Q(i,j)$ is a product of two terms, which is reminiscent of the *Chung-Lu model* given by
$P_{\text{CL}}(A_{ij}=1) = \frac{d_id_j}{2M},$
provided that the network is highly sparse (so that multi-edges are rare and can be neglected). In fact, by a simple adaptation, we can employ an efficient algorithm with complexity of ${\cal O}(M)$ proposed in the following paper:

[Efficient Generation of Networks with Given Expected Degrees | SpringerLink](https://link.springer.com/chapter/10.1007/978-3-642-21286-4_10)

More specifically, we adapt the algorithm by computing $P(A_{ij}=1)$ based on $\exp(f(i,j)) /(1 + \exp(f(i,j)))$ instead of $d_id_j/2M$ in the original form.

# Enhanced configuration model

It is easy to extend the proposed sampling method to the enhanced configuration model. The enhanced configuration model consists of sampling. The enhanced configuration model generates a weighted network based on the following probability:
$P(W_{ij} = w) = \frac{\exp(-(\alpha_i + \alpha_j) 1(w>0) - (\beta_i +\beta_j) w )}{1 -\exp(-\beta_i-\beta_i) + \exp(-\alpha_i - \alpha_j - \beta_i - \beta_j)}$
