# -5k-parameter-model-skeleton-not-trained-

ProbTrajectory5k
A lightweight probabilistic trajectory model (~5k parameters) for exploring low-entropy motion paths through synthetic environments.
This project provides a minimal neural skeleton capable of representing complex trajectory divergence using small-parameter, branch-based latent representations. Designed for research, experimentation, and forward exploration of trajectory synthesis.
Features
Ultra-lightweight: ~5k trainable parameters, suitable for low-resource machines and rapid iteration.
Branching superposition: Multi-branch latent trajectories (num_branches) allow modeling divergence and uncertainty without large attention mechanisms.
Low human bias: Focused on probabilistic motion rather than human language or task-specific outputs.
Flexible latent state: state_dim tunable between 16–64 for experimentation.
Residual consistency: 2–4 residual layers ensure stable propagation of latent states.
Complexified latent representation: Real + imaginary components allow uncertainty tracking and low-entropy pathing.
Time embeddings: Fourier features + linear projections encode continuous-time dynamics.
Readout to 3D space: Converts latent trajectories into observable 3D positions.
Installation (Windows + AMD GPU via ZLUDA)
Install Python >=3.10
Install PyTorch (CPU or CUDA via ZLUDA)
Copy code
Bash
pip install torch torchvision
Add ZLUDA DLLs to your system PATH
Place prob_traj_5k.py in your working directory
Quick Start
Copy code
Python
import torch
from prob_traj_5k import ProbTrajectory5k

# Initialize model
model = ProbTrajectory5k(state_dim=32, layers=3, num_branches=16)

# Example input
t = torch.linspace(0.0, 150.0, steps=300)
P_d = torch.tensor([0.0, 0.0, 0.0])
theta_d = torch.tensor([0.0, 0.0, 0.0])

# Forward pass
pos_super, uncertainty = model(t, P_d, theta_d)

print("pos_super shape:", pos_super.shape)       # (3, T)
print("uncertainty shape:", uncertainty.shape)   # (T,)
Model Parameters
Parameter
Description
Default
state_dim
Dimension of latent state
32
depth
Unrolling depth / number of timestamps
200
layers
Number of residual layers
3
num_branches
Number of latent branches
16
embed_dim
Dimensionality of branch embedding
8
time_feat_dim
Fourier + linear time feature dimension
8
hidden
Hidden size for branch MLP
32
epsilon
Small scalar for complex division stability
0.5
Notes / Next Steps
The model is a skeleton; no training yet. Forward pass demonstrates latent motion propagation.
Suitable for small synthetic datasets or experimental trajectory inputs.
Designed to allow exploration of low-entropy trajectories without attention layers or human bias.
Future work: training objectives, Monte Carlo evaluation, synthetic trajectory datasets, and integration with visualization pipelines.
License
CC0 / Public Domain — free to experiment, fork, and extend.
