# Notes on network analytics for blockchain

A quick review of some papers which used network analytics to understand blockchains better

## TAD
[[Code](https://github.com/tdagraphs/tdagraphs)]		
- published 2021, first paper for anomaly detection on multilayer networks				
- use subgraph approx to alleviate computational load			
- Areas to improve				
    - uses normalized number of transactions between nodes as the edge weights, which sieves out high activity, rather than high value events	
    - small sample size: focuses on 32 events, data is aggregated daily so 152 data points
- robust to perturbations: Looks for changes in global rather than local structure		
		

## Alphacore
[[Code](https://github.com/friedhelmvictor/alphacore)]					
- Core idea: metric that captures a combination of centrality n core decomposition			
- Results				
    - Avg precision (across networks) is ~ 0.54 to label exchanges -- So there are other impt nodes as well!			
        - only using features N_in and N_out: the num of neighbors reachable with in/out edges of that node (NOT degree!). 		
        - neighborhood size and degree are not the same when multi edges are present		
        - They also tried weighted in n out degrees but hurts performance 		
- complexity				
    - n^3 algo where n is num features, O(mnv^2) term too. needs a lot of matrix inversion		
- data prep				
    - edge: transferred token amt. prunes weights that r v small (< max weight / 10^10 ) for efficiency			
    - token networks: only top 100. then prune to tokens that are on >= 10 labelled CEX/ DEX, reducing the avail networks to 28			

## bcheist 		
- Uses TDAmapper algo which can be found [[here](https://github.com/paultpearson/TDAmapper)]		
- Tackles 2 probs: same family pred, new family pred	
- Data
    - uses 24h blocks	
    - uses tx as neighbors rather than other addresses	

## Chartalist
[[Code](https://github.com/cakcora/Chartalist)]		
- Contributions	
    - Curated dataset (previously, data can be hard to download without the right tools)
    - Graph ML ready, with some algorithms evaluated
- Tasks
    - Anomalous Transaction Pattern Detection
        - demonstrated detection of wash trading on ETH DEX, Illicit activity on BTC
    - address (eg exchange) / transaction (eg malicious) type classification
        -  ETH: showed DEX/CEX classification
    - Multilayer Network Analysis: patterns from use of multiple assets. Eg when blockchain is banned in a country
        - analyzed for ETH
    - Coin Tracking Across Blockchains
    - Price Analytics
    - address clustering to identify  which addresses might be the same entity
        - showed Ransomware clustering for BTC
    - stablecoin analysis
        - mainly data, no techniques shown

