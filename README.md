# Skyward tech challenge for AI engineer position

This repository is meant to be used as a challenge for AI engineer candidates at Skyward.
You should fork/clone this repository to use as a basis for the challenge. Once you are done with the challenge, send us a link to your github repository with the final solution and record a short video of the working app.

Subject of this challenge is to develop and deploy a simple, but production ready replica of [Perplexity.ai](https://www.perplexity.ai/).

The requirements are as follows:
* Feel free to use any open-source framework : LlamaIndex, LangChain, Haystack, etc.
* Basic UI.
* Any LLM.
* Any Cloud.
* Should be deployable with scripts (IaC)
* Think about scalability and performance.<br>



Helpers:

- IaC Test account:
  - AWS Free Tier account: <https://aws.amazon.com/free/>
  - Localstack API: <https://localstack.cloud>
- Terraform best practices: <https://cloud.google.com/docs/terraform/best-practices-for-terraform>
- Terraform AWS provider: <https://registry.terraform.io/providers/hashicorp/aws/latest>
- LlamaIndex: <https://www.llamaindex.ai/>
- LangChain: <https://www.langchain.com/>
- Streamlit: <https://streamlit.io/>
- Loom: <https://www.loom.com/>


# Implemetation
To develop and deploy a simple, production-ready replica of [Perplexity.ai](https://www.perplexity.ai/) with components including **Node.js modules**, **backend**, **frontend**, **Terraform**, and **Docker**, follow this step-by-step guide:

### 1. **Project Structure and Requirements**

The project can be broken into the following components:

- **Frontend**: Built with React.js (or any other framework), handling user interactions and communicating with the backend via APIs.
- **Backend**: A Node.js service running Express.js or Fastify for handling API requests. It interacts with a search engine, databases, or AI models.
- **Infrastructure**: Managed with **Terraform** to deploy the infrastructure in AWS (or another cloud provider).
- **Containerization**: Use **Docker** to containerize both frontend and backend applications for easier deployment and scaling.
- **Deployment Pipeline**: Managed via CI/CD pipelines (GitHub Actions, Jenkins, etc.), allowing automated building and deployment.

### 2. **Development Workflow**

#### **Frontend Development**

1. **Setup Frontend Framework**:
   - Used react js framework.
   
   Example with React:
   ```bash
   npx create-react-app perplexity-clone-frontend
   cd perplexity-clone-frontend
   ```

2. **Implement UI Components**:
   - Develop components for the search box, response display, and API interactions.
   - Used **Axios**  for making HTTP requests to the backend API.

3. **Connect to Backend API**:
   - In the frontend, used environment variables to configure the backend URL. Made sure to handle responses from the backend to display search results.

4. **Dockerize the Frontend**
   Create a `Dockerfile` for the frontend
   ** Use Node 16 base image
   FROM node:16

   Set working directory
   WORKDIR /app

  Copy package.json and install dependencies
  COPY package.json .
  RUN npm install

  Copy the rest of the files
  COPY . .

  Expose the port
  EXPOSE 3000

  Start the React application
  CMD ["npm", "start"]

#### **Backend Development**  

1. **Setup Node.js Backend**:
   - Initialized the Node.js backend with fastapi for handling API requests.


2. **Build API Endpoints**:
   - Created a basic API that accepts search queries, calls external APIs on ChatGpt-40 AI model, and returns search results. Used flask, langchain open ai for Chatgpt and CORS for connecting to frontend.

3. **Dockerize the Backend**
  - Create a `Dockerfile` for the backend:
    Use Python 3.9 base image
    FROM python:3.9

    Set working directory
    WORKDIR /app

    Copy the requirements file and install dependencies
    COPY requirements.txt .
    RUN pip install --no-cache-dir -r requirements.txt
    RUN pip install gunicorn

    Copy the rest of the app code
    COPY . .

    Expose the port
    EXPOSE 5000

    Run the application
    CMD ["gunicorn", "--bind", "0.0.0.0:5000", "app:app"]
  

#### **Containerization with Docker**

1. **Build Docker Images**:
   For both frontend and backend, build Docker images using Docker CLI:
   ```bash
   # For Frontend
   docker build -t perplexity-frontend .

   # For Backend
   docker build -t perplexity-backend .
   ```

2. **Push Docker Images to a Registry**:
   Push your images to Docker Hub, AWS ECR, or GitHub Container Registry:
   ```bash
   # Push Frontend
    docker tag 31c81a2ab4d0 ghcr.io/manikbali/dockerimages:latest
    docker push 31c81a2ab4d0 ghcr.io/manikbali/dockerimages:latest

   # Push Backend
   docker tag 2b83d62638d1 ghcr.io/manikbali/dockerimages:latest
   docker push 2b83d62638d1 ghcr.io/manikbali/dockerimages:latest

   ```

### 3. **Infrastructure with Terraform (Deploying on AWS)**

Use **Terraform** to manage the cloud infrastructure. The following AWS components will be created:
  The terraform directory has a main.tf file. This file has task descriptions that can allow users to deploy the infrastructure on the AWS cloud.
  Commands to deploy on the AWS cloud 
  1. terraform init
  2. terraform apply.
  

### 4. **Running Instance**

Clone the repo in your local machine.
give the. In the root directory give the command 
- docker-compose up
- 
One can access the webpage 

Local:            http://localhost:3000
frontend_1  |   On Your Network:  http://172.21.0.2:3000
