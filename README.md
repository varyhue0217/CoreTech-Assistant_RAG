# Multilingual Biodiversity Data Chatbot

## Project Overview

This project focuses on enhancing global access to biodiversity data by creating a multilingual chatbot powered by Retrieval-Augmented Generation (RAG) technology. The chatbot is designed to bridge language gaps and simplify the complex Darwin Core (DWC) standard, making it easier for users to access, understand, and contribute to biodiversity data.

## Features

- **Multilingual Support:** The chatbot can detect and respond in multiple languages, making biodiversity data accessible to non-English-speaking communities.
- **RAG-Enhanced Knowledge:** The chatbot uses RAG technology to retrieve expert-level information from various biodiversity data standards, including Darwin Core.
- **Simplified Data Access:** By converting DWC documents from XML to CSV, the chatbot can better interpret and provide meaningful insights from the data.

## RAG Data Files

The RAG data files used by the chatbot have been preprocessed and are available in the following directory:

1. dwc_csv: DWC Core.(xml → csv file).
2. ext_csv: DWC Extension.(xml → csv file).
3. gbif doc:Documentation from  https://docs.gbif.org/documentation-guidelines/en/#current-documents .pdf file.
4. ipt md: ipt user manual.(xml → md file).

These files have been converted to improve comprehension and usability.

## FlowiseAI Integration

This project is built using [FlowiseAI](https://docs.flowiseai.com/getting-started). The integration with FlowiseAI allows the chatbot to connect with OpenAI's language models and other essential tools, enhancing its ability to process and retrieve biodiversity data.

For setup and detailed instructions on using FlowiseAI, please refer to the official [FlowiseAI documentation](https://docs.flowiseai.com/getting-started).

## Workflow Configuration

The workflow used in this project has been configured and is available in the top-level directory.

## Getting Started

To get started with the project:

1. Follow the instructions provided in the [FlowiseAI documentation](https://docs.flowiseai.com/getting-started) to set up the chatbot environment.
2. Import the workflow to deploy the chatbot.
3. load the RAG data files. 
4. start interacting with multilingual biodiversity data chat bot.
