# transformerXL_PPO_JAX

This repository provides a JAX implementation of TranformerXL with PPO in a RL setup following :  "Stabilizing Transformers for Reinforcement Learning" from Parisotto et al. (https://arxiv.org/abs/1910.06764). 

The code uses the PureJaxRL (https://github.com/luchris429/purejaxrl) template for PPO and copied some of the code from Huggingface transformerXL (https://github.com/huggingface/transformers/blob/v4.40.1/src/transformers/models/deprecated/transfo_xl/modeling_transfo_xl.py) transferring it to JAX.

The training handles Gymnax (https://github.com/RobertTLange/gymnax) environment. 
We also tested it on Craftax ( https://github.com/MichaelTMatthews/Craftax/tree/main/craftax ), on which it beat the baseline presented in the paper (https://arxiv.org/abs/2402.16801) including PPO-RNN, training with unsupervised environment design and intrinsic motivation. 
Notably we reach the 3rd level (the sewer) and obtain several advanced advancements, which was not achieved by the methods presented in the paper. 

The training of a 5M transformer on craftax for 1e9 steps takes about 6h30 on a single A100. 

## Installation

```
git clone git@github.com:Reytuag/transformerXL_PPO_JAX.git
cd transformerXL_PPO_JAX
pip install requirements.txt
```
## Training 

You can edit the training config in train_PPOtrXL.py ( or train_PPOtrXL_pmap.py if you want to go multi GPU) including the name of the environment. (you can put any gymnax environment name, or "craftax" which will use the CraftaxSymbolic env)   

To launch the training: 
```
python3 train_PPOtrXL.py
```
Or if you go multi GPU.(it will use all your GPU) 
```
python3 train_PPOtrXL_pmap.py
```

## Results on Craftax 

Without much parameter search, with a budget of 1e9 timesteps, the normalized return (max) achieve 18.5 compared to 15.3 for PPO-RNN according to the craftax paper. (with one seed visiting the sewer). 

With a budget of 4e9 timesteps, ... 

## Related Works 
* Gymnax: https://github.com/RobertTLange/gymnax
* Craftax: https://github.com/MichaelTMatthews/Craftax
* Xland-Minigrid: https://github.com/corl-team/xland-minigrid
* PureJaxRL: https://github.com/luchris429/purejaxrl
* JaxMARL: https://github.com/FLAIROx/JaxMARL
* Jumanji: https://github.com/instadeepai/jumanji
* Evojax: https://github.com/google/evojax
* Evosax: https://github.com/RobertTLange/evosax
* Brax: https://github.com/google/brax


## Next steps 

* Train it on XLand-MiniGrid (https://github.com/corl-team/xland-minigrid) to test it on an open-ended environment in a meta-RL fashion.
* Add an implementation of Muesli (https://arxiv.org/abs/2104.06159) with transformerXL as in "Human-Timescale Adaptation in an Open-Ended Task Space" (https://arxiv.org/abs/2301.07608)



