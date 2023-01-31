# economic_games_chatgpt

## Setting up the repository

We use Python version 3.10.8 to create a virtual environment to be used in this project

```
python3.10 -m venv .venv
source .venv/bin/activate # (for mac/linux users)
# source .venv/Scripts/Activate (for windows users)

(.venv) pip install --upgrade pip
(.venv) pip install wheel
(.venv) pip install -r requirements.txt
```

## Using ChatGPT with the OpenAI API

The OpenAI API makes it possible to send a request to ChatGPT language models and obtain a response back. In order to 
use the API an OpenAI account is necessary. An API key is also needed in order to use the API (more info here: https://beta.openai.com/docs/api-reference/authentication).
Once you have an OpenAI account and have obtained an API key associated to the account create a `.env` file in the root folder
of the repository 

```
OPENAI_API_KEY=<your_api_key_here>
```

## Running the analysis script

In order to run the analysis script `ai_participant.py` specify the economic game and the action you want to perform.
Economic game can be one of the following options:

* `ultimatum_sender` (sender perspective)
* `ultimatum_receiver` (receiver perspective)
* `dictator`
* `trust_sender` (sender perspective)
* `trust_receiver` (receiver perspective)

The action to perform can be one of the following options:

* `test_assumptions` (this action sends prompts that test the language model's knowledge of the selected game and checks for the assumptions that the language model has on the game dynamics)
* `send_prompts` (this action sends prompts for a specific game)

E.g. run the script on the trust game from the sender perspective, send all prompts to the language model and save responses
```
(.venv) python ai_participant.py --game trust_sender --mode send_prompts
```

## Factor Levels for prompts

For each game a parameter file in the `params` folder of the repository is created.
The parameter file contains all prompts used in the study, organized by different languages and by prompt type (baseline or experimental).
Additionally, the parameter file includes all factors and language model parameters that are used in the study.
Parameters used include:

### Across all games, baseline and experimental prompts
| Parameter Name | Type  | Levels                              |
|----------------|-------|-------------------------------------|
| Temperature    | float | [0.4, 0.7, 1] (low, medium, high)   |
| Language       | str   | [EN, ...]                           |
| Amount         | int   | [10, 100, 1000] (low, medium, high) |

### Across all games, experimental prompts
| Parameter Name | Type | Levels                           |
|----------------|------|----------------------------------|
| Age            | int  | [20, 50, 70] (low, medium, high) |
| Gender         | str  | [male, female, non-binary]       |
