# TGtrader
<br>
TG Trader was deisgned with idea to replace chart operator with active trade management of tens or hundreds of positions simultaneously while receving json data from multiple sources such as Tradingview Alerts<br><br>
Currrently only opening positions in one direction and flippening.Hedge mode is not currently supported.<br>
Trailing orders are available on ByBit but not supported at this time, see TODO list.<br><br>
Best way to run as docker container either localy or remotely with Docker Desktop/Server + Docker Compose plugin.<br>
MS VS Code with needed plugins is a front end tool for container management for me at this time but there are also multiple <br>
options to do that .<br><br>
Risk/Money Management model in terms of Take profit and Stop loss points is supplied by signal source but it is also flexible as there <br>
are at least 2 timeframes with 2 different types of market (flat / trending) <br> <br>
After each posistion passes specific PNL%, entire position will be moved to break even(BE): SL price will be set to position entry price.<br>
If you just want to open some position without MM, or if any errors occur during TP/SL orders submission, default TP and SL orders will be<br>
submitted in internal loop cycle for your convenience with default trade management follow up .<br><br>
For further PNL tracking follow up received signals are stored locally in json format and can imported to database like MongoDB for further analysis.<br><br>
Bot will trade in opposite direction (flip) if it has position opened is similar direction and will not open just another plain market order. <br> 
Risk management model I personally follow from my signals channels doesn't provide any averaging down or adding into position at this time <br>
But you can add into existing position with sending market opder webhook while specifying [average down] instead of [market order] any time.

 1. Actual order entry from webhook source in Testnet ([https://www.youtube.com/watch?v=vQ3hkkFoEwA](https://www.youtube.com/watch?v=vQ3hkkFoEwA))
 2. Order management process in live account ([https://www.youtube.com/watch?v=KCOpB7cqE-0](https://youtu.be/KCOpB7cqE-0))

##### Disclaimer: This project is for bug testing requests, extentions and features requests .

Currently supported exchanges:

- **Bybit** futures ([https://bybit.com](https://www.bybit.com/en/)) 
- **Bybit** futures Testnet([https://testnet.bybit.com](https://www.testnet.bybit.com/en/))

### INSTALLATION AND RUNNING ###

##### Any platform :

- Download and install Docker desktop and MS VScode.<br> 
- Unpack docker images and start main docker containeer using docker-compose file as shown on video 1.<br>

With these you can start receiving webhooks signals, but if you don't have en external IP address than your instance will<br>
not be visible to Trading View or other sources if planning to receive external signals .<br>
My own source signal is called TGclient as shown in the same vid and is running in the same network in another docker conatiner<br>

To get your server visible over the web you can install something like: <br> 
 - [DYNDNS in another docker container](https://hub.docker.com/r/blaize/docker-dynamic-dns/#!) <br> 
 - [Ngrok](https://ngrok.com/download). <br> 
 Or some other kind of proxy.<br> 

This essentually will bring you to miscoservices infrastructure that can be easily moved between hosting/cloud VPS providers and is managed by docker compose.<br>

- All operations with stop and start , checking logs etc.. are standard for any docker container. <br>
You can have unlimited number of intances inside single docker-compose file. <br>

### SIGNAL SYNTAX ###
 
Signals format is 100% compatible with Cornix Telegram bot (As far as I can see) <br>

- **Open market**

{ <br>
 "symbol": "BELUSDT",
 "direction": "LONG",
 "position_size": "15",
 "leverage": "10.0",
 "tp_price1": "0.6195",
 "tp_price2": "0.6226",
 "tp_price3": "0.6256",
 "tp_price4": "0.6287",
 "tp_price5": "0.6349",
 "tp_price6": "0.6411",
 "tp_price7": "0.6472",
 "tp_price8": "0.6534",
 "tp_price9": "0.6657",
 "sl_price": "0.6041",
 "action": "open market",
 "market_price": "0.6164"
} <br>

- **Open limit**


{ <br>
 "symbol": "BELUSDT",
 "direction": "LONG",
 "position_size": "15",
 "leverage": "10.0",
 "tp_price": "0.6395", 
 "sl_price": "0.5041"
 "action": "open limit",
 "limit_price1": "0.6164"
 "limit_price2": "0.6004" 
 "limit_price3": "0.5564"
 "limit_price4": "0.5164"
} <br>

- **Close market**

{ <br>
 "symbol": "BELUSDT",
 "direction": "LONG",
 "action": "close market",
 "close_perc": "100 or any"
} 
 

### CONFIGURATION - API KEYS ###
You can try to use my testnet instance or create you own either live or testnet as shown below in tgtrader.yml

&emsp;
&emsp;&emsp;		# Testnet instance API keys
&emsp;&emsp;		api_key: "your API_key"<br>
&emsp;&emsp;		api_secret: "your API secret"<br>
&emsp;&emsp;		Testnet: True|False<br><br>
&emsp;	


### KNOWN BUGS ### 
- I cleaned most of the bugs I have noticed for last couple month while running live trades and looking for your additional feedback.


### TO DO LIST ### 
- With using multiple threads and flask in async mode - still facing performance bottlnecks shat shouldn't be there, need to check further
- Migration to other exchanges.
- Web interface .<br>
- I was trying to implement WebSockets from ByBit but that caused IP banning problem for some reason and I didn't have time to investigate, That internal loop is a sort of a workaround
- Telegram email /alerting implementation is in progress
- Not sure if this will have same execution speed with CCXT

### Q&A ###
Pls reach out to me via email or here
