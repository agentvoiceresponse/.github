# Agent Voice Response (AVR)

The **Agent Voice Response (AVR)** [agentvoiceresponse.com](https://www.agentvoiceresponse.com/) is an advanced IVR solution that integrates with AI, providing a voicebot interface through Asterisk's AudioSocket application. This architecture allows for the replacement of traditional IVR systems with AI-powered conversational agents.

## Table of Contents
- [Overview](#overview)
- [Example Flow](#example-flow)
- [Features](#features)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Usage](#usage)
- [Troubleshooting](#troubleshooting)
- [Community](#community)
- [Contributions](#contributions)
- [License](#license)

## Overview

AVR Core manages real-time voice communication between customers and a Asterisk AudioSocket application and interacts with various AI services:

1. **ASR (Automatic Speech Recognition)**: Transcribes the incoming audio stream from the customer into text 
2. **LLM (Large Language Model)**: Interprets the text and generates an appropriate response. 
3. **TTS (Text-to-Speech)**: Converts the generated text response back into speech, which is then played to the customer. 

AVR Core is designed to be flexible, allowing users to integrate any ASR, LLM, and TTS services by interacting via HTTP API Streams. This modularity allows you to develop your own middleware between AVR Core and the services of your choice.

### Example Flow:

<div align="center">
  <a href="https://github.com/agentvoiceresponse/.github/blob/main/profile/images/avr-architecture.mp4">
    <img src="https://github.com/agentvoiceresponse/.github/blob/main/profile/images/avr-architecture.png" alt="AVR Architecture Video" width="600">
    <br>
    <em>Click to watch the AVR architecture video</em>
  </a>
</div>

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

## Prerequisites

Before installing AVR, ensure you have the following components:

- Docker and Docker Compose
- An Asterisk server with AudioSocket module enabled
- Access and credentials to ASR, LLM, and TTS services 

## Installation

1. **Clone the AVR Infrastructure**: 
   - Clone the `avr-infra` repository from [https://github.com/agentvoiceresponse/avr-infra](https://github.com/agentvoiceresponse/avr-infra).

2. **Set Environment Variables**:
   - Configure the following environment variables in your `.env` file:
     ```bash
     NODE_ENV=production
     APP_VERSION=1.0.0
     PORT=3000
    
     ADMIN_EMAIL=YOUR_EMAIL
     ADMIN_PASSWORD=YOUR_PASSWORD
    
     DATABASE_HOST=127.0.0.1
     DATABASE_PORT=3306
     DATABASE_NAME=avr-app
     DATABASE_USERNAME=avr
     DATABASE_PASSWORD=MYSQL_PASSWORD
     
     DATABASE_ROOT_PASSWORD=MYSQL_ROOT_PASSWORD
     ```

3. **Run Docker Compose**:
   - Navigate to the project directory and run:
     ```bash
     docker-compose up
     ```

## Usage

Enjoy the Agent Voice Response App experience! After installation, you can access the application through your browser.

<div align="center">
  <img src="https://github.com/agentvoiceresponse/.github/blob/main/profile/images/avr-login.png" alt="Login Screen" width="600">
  <br>
  <em>The secure login interface for the AVR application</em>
</div>

<div align="center">
  <img src="https://github.com/agentvoiceresponse/.github/blob/main/profile/images/avr-dashboard.png" alt="Dashboard" width="600">
  <br>
  <em>The intuitive dashboard for managing your voice response agents</em>
</div>

## Troubleshooting

If you encounter issues during installation or usage:

1. **Connection Issues**:
   - Ensure all services are running with `docker-compose ps`
   - Check logs for specific errors: `docker-compose logs avr-core`

2. **Audio Quality Issues**:
   - Verify the audio codec settings in Asterisk
   - Check the ASR service compatibility with your audio format

3. **Performance Issues**:
   - Consider scaling resources for components handling high traffic
   - Optimize LLM prompts for faster response times

## Community

Join our growing community of developers and users to share ideas, get help, and collaborate on projects:

- [Discord Server](https://discord.gg/MUd3y7eGVF) - Connect with other AVR users and the development team

## Contributions

For those who wish to contribute to the project, please send an email to [info@agentvoiceresponse.com](mailto:info@agentvoiceresponse.com).

## License

Agent Voice Response (AVR) is released under the MIT License. See the LICENSE file for details.
