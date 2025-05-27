# Agent Voice Response (AVR)

[![Discord](https://img.shields.io/discord/1347239846632226998?label=Discord&logo=discord)](https://discord.gg/DFTU69Hg74)

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
- [License](#license)

## Overview

AVR Core manages real-time voice communication between customers and a Asterisk AudioSocket application and interacts with various AI services:

1. **ASR (Automatic Speech Recognition)**: Transcribes the incoming audio stream from the customer into text 
2. **LLM (Large Language Model)**: Interprets the text and generates an appropriate response. 
3. **TTS (Text-to-Speech)**: Converts the generated text response back into speech, which is then played to the customer. 
4. **STT (Speech-to-Text)**: Provides accurate transcription of spoken language into text, supporting multiple languages and dialects.
5. **STS (Speech-to-Speech)**: Enables direct voice-to-voice communication with AI agents, creating natural and fluid conversations.


AVR Core is designed to be flexible, allowing users to integrate any ASR, LLM, and TTS services by interacting via HTTP API Streams. This modularity allows you to develop your own middleware between AVR Core and the services of your choice. In recent versions, AVR Core has been enhanced with STT (Speech-to-Text) integration to support providers that don't yet offer ASR capabilities, and STS (Speech-to-Speech) integration for direct connection with Conversational AI services like OpenAI Realtime, bypassing the need for separate ASR, LLM, and TTS components.

### Example Flow with ASR, LLM and TTS:

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
- **Multi-language support**: Handle conversations in multiple languages.
- **Customizable voice personalities**: Configure different voice characteristics for your AI agents.
- **Detailed analytics**: Monitor and analyze call metrics and performance.
- **Secure communication**: End-to-end encryption for all voice and data streams.

For a list of available integrations, check [Agent Voice Response Integrations](https://github.com/orgs/agentvoiceresponse/repositories).

## Prerequisites

Before installing AVR, ensure you have the following components:

- Docker and Docker Compose
- An Asterisk server with AudioSocket module enabled
- Access and credentials to ASR, LLM, and TTS services 

## Installation

1. **Clone the AVR Infrastructure**  
   Clone the `avr-infra` repository from the official GitHub repository:

   ```bash
   git clone https://github.com/agentvoiceresponse/avr-infra.git
   cd avr-infra

2. **Follow the Instructions in the README**
   Inside the cloned repository, follow the setup and configuration steps described in the README.md file to launch your AVR agent with the desired ASR, LLM, and TTS providers.

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
   - Verify network connectivity between services

2. **Audio Quality Issues**:
   - Verify the audio codec settings in Asterisk
   - Check the ASR service compatibility with your audio format
   - Ensure proper audio device configuration

3. **Performance Issues**:
   - Consider scaling resources for components handling high traffic
   - Optimize LLM prompts for faster response times
   - Monitor system resource usage

4. **Common Solutions**:
   - Check our [Troubleshooting Guide](https://wiki.agentvoiceresponse.com)
   - Review the [FAQ](https://agentvoiceresponse.com/#faqs)


## Community

Join our growing community of developers and users to share ideas, get help, and collaborate on projects:

- [Discord Server](https://discord.gg/MUd3y7eGVF) - Connect with other AVR users and the development team
- [Documentation Wiki](https://wiki.agentvoiceresponse.com) - Comprehensive guides and tutorials
- [Website](https://www.agentvoiceresponse.com) - Latest updates and feature announcements


## License

Copyright (c) 2024 Agent Voice Response

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
