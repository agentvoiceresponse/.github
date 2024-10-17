# Agent Voice Response (AVR)

The **Agent Voice Response (AVR)** [agentvoiceresponse.com](https://www.agentvoiceresponse.com/) is an advanced IVR solution that integrates with AI, providing a voicebot interface through Asterisk's AudioSocket application. This architecture allows for the replacement of traditional IVR systems with AI-powered conversational agents.

## Overview

AVR Core manages real-time voice communication between customers and a Asterisk AudioSocket application and interacts with various AI services:

1. **ASR (Automatic Speech Recognition)**: Transcribes the incoming audio stream from the customer into text (Google Speech to Text)
2. **LLM (Large Language Model)**: Interprets the text and generates an appropriate response. (OpenAI / Typebot)
3. **TTS (Text-to-Speech)**: Converts the generated text response back into speech, which is then played to the customer. (Google Text to Speech)

AVR Core is designed to be flexible, allowing users to integrate any ASR, LLM, and TTS services by interacting via HTTP API Streams. This modularity allows you to develop your own middleware between AVR Core and the services of your choice.

### Example Flow:
- Asterisk sends the audio stream to the AVR Core.
- AVR Core forwards the audio to an ASR service for transcription (e.g., `ASR_URL=http://localhost:6001/speech-to-text-stream`).
- Once transcription is received, AVR Core sends the text to an LLM service (e.g., `LLM_URL=http://localhost:6005/prompt-stream`).
- The LLM generates a response, which is sent to a TTS service for voice synthesis (e.g., `TTS_URL=http://localhost:6003/text-to-speech-stream`).
- The synthesized voice is played back to the customer via Asterisk.

## Features
- **Plug-and-play architecture**: Easily swap out different ASR, LLM, and TTS services.
- **Real-time voice-to-text and text-to-voice streaming**: Handles customer interactions seamlessly via HTTP API streams.
- **Scalable design**: Integrate your own AI services using custom middleware.
  
For a list of available integrations, check [Agent Voice Response Integrations](https://github.com/orgs/agentvoiceresponse/repositories).

## Installation

1. **Clone the AVR Infrastructure**: 
   - Clone the `avr-infra` repository from [https://github.com/agentvoiceresponse/avr-infra](https://github.com/agentvoiceresponse/avr-infra).

2. **Set Environment Variables**:
   - Configure the following environment variables in your `.env` file:
     - `ASR_URL`: URL of the ASR service (e.g., Google Cloud Speech-to-Text).
     - `LLM_URL`: URL of the LLM service (e.g., OpenAI or Typebot).
     - `TTS_URL`: URL of the TTS service (e.g., Google Cloud Text-to-Speech).
     - `WALLET_ID`: Your wallet ID for production use (1 credit = 1 EUR = 100 minutes of usage).

3. **Run Docker Compose**:
   - Navigate to the project directory and run:
     ```bash
     docker-compose up
     ```

## Usage

### Free Version
In the free version, each call is limited to **1 minute** of interaction. For extended usage, please contact us at [info@agentvoiceresponse.com](mailto:info@agentvoiceresponse.com) to set up your wallet.

### Production Use
To use AVR Core in production, contact us at [info@agentvoiceresponse.com](mailto:info@agentvoiceresponse.com). We will provide you with a `WALLET_ID`, allowing you to manage credits and usage.

## Contributions

For those who wish to contribute to the project, please send an email to [info@agentvoiceresponse.com](mailto:info@agentvoiceresponse.com).
