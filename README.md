# HyDE Main Functions Documentation

## Overview
This document explains the functions in `main.py`, which handles toy product data processing and Elasticsearch operations.

## Functions

### get_ai_completion(prompt)
Makes API calls to OpenAI's GPT model to generate completions based on provided prompts.

**Parameters:**
- `prompt`: String containing the text prompt to send to the AI model

**Returns:**
- OpenAI API completion response object

### generate_prompt(row)
Generates an AI prompt from product data to create a detailed query profile.

**Parameters:**
- `row`: Dictionary containing product details (name, description, price, target age)

**Returns:**
- String containing formatted prompt for AI completion

### export_toys_to_json()
Reads toy data from CSV file, enriches it with AI-generated query profiles, and exports to JSON.

**Dependencies:**
- Requires toys.csv input file
- Creates toys.json output file

### create_index()
Creates an Elasticsearch index with predefined mappings for toy product data.

**Index Properties:**
- product_name (text)
- product_description (text) 
- price (float)
- target_age (integer)
- query_profile (sparse_vector)
- raw_query_profile (text)

### create_ingest_pipeline()
Sets up an Elasticsearch ingest pipeline using the ELSER model for processing query profiles.

### create_inference_endpoint() 
Configures the ELSER inference endpoint for sparse embedding generation.

### load_index()
Bulk loads toy data from JSON file into Elasticsearch index.

**Dependencies:**
- Requires toys.json input file
- Uses elser-v2 pipeline

### find_a_toy(query_string)
Searches the toy index using ELSER embedding model.

**Parameters:**
- `query_string`: Search query text

**Returns:**
- Top 3 matching toy results with product name, price and target age

### add_one_toy(toy)
Adds a single toy product to the index with AI-generated query profile.

**Parameters:**
- `toy`: Dictionary containing toy product details

### delete_index()
Removes the Elasticsearch index if it exists.