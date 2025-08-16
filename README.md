# Docker Model Runner - Dockerized v2

A containerized Streamlit application that provides a web interface for interacting with local Large Language Models (LLMs) through Docker. This project demonstrates how to run AI models locally using Docker containers with a user-friendly web interface.

## 🚀 Features

- **Web-based Chat Interface**: Clean Streamlit UI for interacting with LLMs
- **Local Model Support**: Run AI models locally without external API dependencies
- **Docker Containerization**: Easy deployment and consistent environment across different systems
- **Environment Configuration**: Flexible configuration through environment variables
- **Real-time Responses**: Interactive chat experience with streaming responses

## 🏗️ Architecture

The project consists of two main services:

1. **App Service**: Streamlit web application container
2. **LLM Service**: Local language model service using Ollama

```
┌─────────────────┐    ┌─────────────────┐
│   Streamlit     │    │   Local LLM     │
│   Web App       │◄──►│   (Ollama)      │
│   (Port 8501)   │    │                 │
└─────────────────┘    └─────────────────┘
```

## 📋 Prerequisites

- Docker and Docker Compose installed on your system
- At least 4GB of available RAM (for running LLMs)
- Internet connection for initial Docker image downloads

## 🛠️ Installation & Setup

### 1. Clone the Repository

```bash
git clone <repository-url>
cd docker-model-runner-dockerized-v2
```

### 2. Configure Environment Variables

The application uses environment variables for configuration. You can modify the `backend.env` file:

```env
BASE_URL=http://host.docker.internal:12434/engines/llama.cpp/v1/
MODEL=ai/smollm2:latest
OPENAI_API_KEY=dockermodelrunner
```

**Configuration Options:**
- `BASE_URL`: URL for the Ollama API endpoint
- `MODEL`: Name of the LLM model to use
- `OPENAI_API_KEY`: API key for authentication (can be any value for local models)

### 3. Start the Services

```bash
docker-compose up --build
```

This command will:
- Build the Streamlit application container
- Pull and start the LLM service
- Expose the web interface on port 8501

### 4. Access the Application

Open your web browser and navigate to:
```
http://localhost:8501
```

## 🎯 Usage

1. **Enter Your Prompt**: Type your question or request in the text area
2. **Submit**: Click the "Submit" button to generate a response
3. **View Response**: The AI model's response will appear below the input area

### Example Prompts

- "Explain quantum computing in simple terms"
- "Write a short poem about artificial intelligence"
- "What are the benefits of containerization?"
- "Explain the theory of relativity"

## 🔧 Customization

### Changing the LLM Model

To use a different model, modify the `MODEL` variable in `backend.env`:

```env
MODEL=llama2:7b
```

Available models depend on what you have installed in Ollama. Common options include:
- `llama2:7b` - Llama 2 7B parameter model
- `mistral:7b` - Mistral 7B model
- `codellama:7b` - Code-focused Llama model

### Modifying the Web Interface

The Streamlit application code is located in `app/main.py`. You can customize:
- Page title and styling
- Input field behavior
- Response formatting
- Additional UI components

### Adding Dependencies

To add new Python packages, edit `app/requirements.txt` and rebuild the container:

```bash
docker-compose down
docker-compose up --build
```

## 🐛 Troubleshooting

### Common Issues

1. **Port Already in Use**
   ```bash
   # Check what's using port 8501
   lsof -i :8501
   
   # Kill the process or change the port in docker-compose.yml
   ```

2. **Model Not Found**
   - Ensure the model name in `backend.env` matches an available Ollama model
   - Check Ollama service logs: `docker-compose logs llm`

3. **Container Build Failures**
   - Clear Docker cache: `docker system prune -a`
   - Rebuild without cache: `docker-compose build --no-cache`

4. **Memory Issues**
   - Ensure sufficient RAM is available
   - Consider using smaller models for limited resources

### Logs and Debugging

View service logs:
```bash
# All services
docker-compose logs

# Specific service
docker-compose logs app
docker-compose logs llm
```

## 📁 Project Structure

```
docker-model-runner-dockerized-v2/
├── app/
│   ├── Dockerfile          # Streamlit app container definition
│   ├── main.py            # Main Streamlit application
│   └── requirements.txt   # Python dependencies
├── backend.env            # Environment configuration
├── docker-compose.yml     # Service orchestration
├── .gitignore            # Git ignore patterns
└── README.md             # This file
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🙏 Acknowledgments

- [Streamlit](https://streamlit.io/) for the web framework
- [Ollama](https://ollama.ai/) for local LLM support
- [Docker](https://www.docker.com/) for containerization

## 📞 Support

If you encounter any issues or have questions:

1. Check the troubleshooting section above
2. Review the logs using `docker-compose logs`
3. Open an issue on the project repository
4. Ensure your system meets the prerequisites

---

**Happy AI Chatting! 🤖✨**
