# alexa-radiothermostat Lambda Fork

This is a NodeJS AWS Lambda script to integrate with [Radio Thermostats](http://www.radiothermostat.com/). 

This is a fork inteded to work with AWS Lambda instead of a dedicated NodeJS and contains updated Alexa intents defintions.

This project is based on the original creation by [bbrookfield](https://github.com/bbrookfield)

#### Getting started
1. Create an AWS Lambda Function and use the included index.js file as the contents of the function. Update the endpoint variable to point to your thermostat's IP address. Ideally, you would access your thermostat's ip from Lambda across a private vpn connection through your VPC's private subnet. But, you can also reference your public ip address and forward traffic to your thermostat (less secure).  
2. Create a new AWS Lambda Layer associated with the function and upload a zip with the required structure and referenced node modules. \nodejs\node_modules\*
4. Setup your Alexa skill
5. Configure your intents (see below)
6. Associate your Lambda Function to trigger from Alexa Skills kit and reference your AWS Lambda function within the Alexa Skills Console by providing the AWS Lambda Function ARN
  
  ```
{
    "interactionModel": {
        "languageModel": {
            "invocationName": "home thermostat",
            "intents": [
                {
                    "name": "AMAZON.FallbackIntent",
                    "samples": []
                },
                {
                    "name": "AMAZON.CancelIntent",
                    "samples": []
                },
                {
                    "name": "AMAZON.HelpIntent",
                    "samples": []
                },
                {
                    "name": "AMAZON.StopIntent",
                    "samples": []
                },
                {
                    "name": "AMAZON.NavigateHomeIntent",
                    "samples": []
                },
                {
                    "name": "getTemp",
                    "slots": [],
                    "samples": [
                        "tell me temperature",
                        "tell me the temperature",
                        "say the temperature",
                        "what's the temperature",
                        "what is temperature",
                        "what is the temperature",
                        "get temperature",
                        "temperature"
                    ]
                },
                {
                    "name": "setHeat",
                    "slots": [
                        {
                            "name": "setHeating",
                            "type": "AMAZON.NUMBER"
                        }
                    ],
                    "samples": [
                        "to set heat to {setHeating}",
                        "to adjust heat to {setHeating}"
                    ]
                },
                {
                    "name": "setCool",
                    "slots": [
                        {
                            "name": "setCooling",
                            "type": "AMAZON.NUMBER"
                        }
                    ],
                    "samples": [
                        "to adjust cool to {setCooling}",
                        "to set cool to {setCooling}",
                        "to adjust air conditioning to {setCooling}",
                        "to set air conditioning to {setCooling}",
                        "to set air to {setCooling}",
                        "to adjust air to {setCooling}",
                        "to adjust the air conditioning to {setCooling}",
                        "to set ac to {setCooling}",
                        "to adjust ac to {setCooling}",
                        "to set air conditioning to {setCooling}"
                    ]
                },
                {
                    "name": "incTemp",
                    "slots": [
                        {
                            "name": "increaseTemp",
                            "type": "AMAZON.NUMBER"
                        }
                    ],
                    "samples": [
                        "raise target temperature by {increaseTemp}",
                        "increase target temperature by {increaseTemp}",
                        "increase temperature by {increaseTemp}",
                        "raise temperature by {increaseTemp}"
                    ]
                },
                {
                    "name": "decTemp",
                    "slots": [
                        {
                            "name": "decreaseTemp",
                            "type": "AMAZON.NUMBER"
                        }
                    ],
                    "samples": [
                        "lower target temperature by {decreaseTemp}",
                        "decrease target temperature by {decreaseTemp}",
                        "decrease temperature by {decreaseTemp}",
                        "lower temperature by {decreaseTemp}"
                    ]
                },
                {
                    "name": "setOff",
                    "slots": [],
                    "samples": [
                        "off",
                        "turn off",
                        "to turn off",
                        "to turn off thermostat",
                        "to turn thermostat off",
                        "to turn the thermostat off",
                        "set thermostat to off",
                        "thermostat off"
                    ]
                },
                {
                    "name": "setOn",
                    "slots": [],
                    "samples": [
                        "on",
                        "turn on",
                        "to turn on",
                        "to turn on thermostat",
                        "to turn thermostat on",
                        "to turn the thermostat on",
                        "set thermostat to on",
                        "thermostat on"
                    ]
                },
                {
                    "name": "setFanOn",
                    "slots": [],
                    "samples": [
                        "to turn on fan",
                        "to turn on blower",
                        "to turn blower on",
                        "to turn fan on",
                        "to turn the blower on",
                        "to turn the fan on",
                        "to set fan to on",
                        "to set blower to on"
                    ]
                },
                {
                    "name": "setFanAuto",
                    "slots": [],
                    "samples": [
                        "to turn off fan",
                        "to turn off blower",
                        "to turn blower off",
                        "to turn fan off",
                        "to turn the blower off",
                        "to turn the fan off",
                        "to set fan to off",
                        "to set blower to off"
                    ]
                },
                {
                    "name": "setHoldOn",
                    "slots": [],
                    "samples": [
                        "to turn on hold",
                        "to turn hold on",
                        "to turn hold on"
                    ]
                },
                {
                    "name": "setHoldOff",
                    "slots": [],
                    "samples": [
                        "to turn off hold",
                        "to turn hold off",
                        "to set hold to off"
                    ]
                }
            ],
            "types": []
        }
    }
}
  ```

