# Offer management

[1. Creating an offer](#1-creating-an-offer)

## 1. Creating an offer
To create an offer, use `create_offer` and pass these parameters:
* address of the entity making the offer - `from_address`, 
* address of the entityto whom the offer is made - `to_address`, 
* name and quantity of asset asked for - `ask_asset` 
* name and quantity of asset offerred in return - `offer_asset`
```
{
  "from_address": "1AQEmkoH7RYBRqAbamLBCTDzGAfjUkJkHwwhpr",
  "to_address": "1NQ81NxvnYH95Gk9jXYAoDBRR42wHb3Bq441gt",

  "ask_asset": 
  	{
    	"USD": 1
  	},

  "offer_asset": 
  	{
    	"INR": 60
  	}
}
```
