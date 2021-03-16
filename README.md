# Docker Images
## ESPN-BOXSCORES
- Zap Oracle that uses ESPN's api to query for boxscore of a basketball match passed in query. It responds with format [awayTeam awayScore | homeScore homeTeam].
- It implements `https://github.com/zapproject/zap-oracle-template` using a custom Responder.ts file.
### Requirements: 
- Have Mnemonic for wallet, with ETH to fullfill queries
- Determine information about your ESPN-Boxscores Oracle, such as : 
    + Title
    + Public key
    + Endpoint's name
    + Endpoint's curve
    + Description for md
    + Query list for endpoint
    
### Build image locally
- `cd ESPN-Boxscores`
- `docker build . --no-cache -t zap-coingecko`

<!-- ### Optional to push image to dockerhub
- `docker image push zap-coingecko`
### Run image
- To run the container , create a local `Config.json` with following format and information about the Oracle (Mnemonic, publid key, title, Endpoint schema and curve for each...)
```
{
	"title": "Signals",
	"public_key": "",
	"NODE_URL": "wss://kovan.infura.io/ws/v3/{PROJECT_ID}", //KOVAN or MAINNET HERE
	"mnemonic": "",
	"EndpointSchema": {
		"name": "btcprice",
		"curve": [
			2,
			1,
			2,
			100000
		],
		"broker": "",
		"md": "CoinGecko prices oracle",
		"queryList": [
			{
				"query": "<pair>",
				"params": [],
				"dynamic": false,
				"responseType": "[int]"
			}
		]
	}
}
```
- Mount the local config file to the container with following command: 
    + `docker run --mount type=bind,source="$(pwd)"/path_to_local_file/Config.json,target=/zap/zap-oracle-template/Oracle/Config.json zap-coingecko`
### Result :
Container will:  
- Create Oralce and Endpoint if not exists in Zap Registry
- Push information such as description and and query list to ipfs which will be displayed on zap admin site
- Listen to query with format of (`coin_name`) (coin's name has to be in the list of coingecko coins list )
    + Example ("bitcoin")
- Respond with coin's usd price -->
