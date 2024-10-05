# Negotiation Bot using Google Generative AI (Gemini)

This project implements a negotiation bot that simulates price negotiations for various products using Google's Generative AI, specifically the Gemini model. The bot is designed to offer flexible pricing while adhering to predefined business rules, such as ensuring the product isn't sold below a certain minimum price.

## Features

- **Product Price Negotiation**: The bot interacts with users to negotiate prices within a set range (list price to minimum price).
- **Human-like Conversations**: Uses Google's Gemini model to generate natural language responses during negotiation.
- **Flexible Pricing Logic**: Allows counter-offers and negotiations up to a predefined limit.
- **End of Negotiation**: Ends the conversation if a valid offer is accepted or after three invalid offers are made.

## How it Works

1. **Model Integration**: 
   The bot uses the Gemini model by fetching an API key securely from Google Colab secrets.

   ```python
   api_key = userdata.get('Gemin_API_Key')
   genai.configure(api_key=api_key)
   model = genai.GenerativeModel('gemini-pro')
   ```

   This API key allows the bot to communicate with Google's generative AI model, producing human-like responses during negotiation.

2. **Pricing Logic**:
   - Each product has a list price and a minimum price that the bot can negotiate down to.
   - The bot generates counter-offers within the range between the list price and the minimum price.

   Example of product data:
   ```python
   products = {
       "laptop": {
           "name": "QuantumX Pro",
           "description": "Ultra-lightweight laptop with AI-enhanced computing power.",
           "list_price": 1350,
           "min_price": 1300,
       }
   }
   ```

   - If the user’s offer is too low, the bot will offer a counter within the allowed price range.
   - The negotiation ends if the user makes three consecutive low offers or a valid offer is accepted.

## Pseudocode for Negotiation Logic

```text
1. Initialize product, minimum price, list price, and a random conversation enhancer.
2. Extract user's offer:
   - If invalid, prompt user for a valid offer.
3. If the offer is below the minimum price:
   - Increment low offer count.
   - If three invalid offers, end the negotiation.
   - Otherwise, generate a counter-offer.
4. If the offer is valid:
   - Accept if it matches or exceeds the list price.
   - If it meets or exceeds the current counter-offer, accept.
   - Else, propose a new counter-offer between the user’s offer and the bot’s offer.
5. Update conversation history and return response.
```

## Usage

1. Clone the repository or download the script.
2. Set up the Colab environment and ensure the Gemini API key is stored as a secret.
3. Run the `negotiation_bot.py` script in Colab or your preferred environment.

## Requirements

- Python 3.x
- Google Colab (for API key storage and execution)
- `google.generativeai` library

