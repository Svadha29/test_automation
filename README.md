# FastAPI Docker Deployment with CI/CD 🚀

A FastAPI application containerized with Docker and automated using GitHub Actions for seamless deployment to Docker Hub.

## 📌 Features
✅ FastAPI web server with RESTful endpoints  
✅ Docker containerization for easy deployment  
✅ GitHub Actions CI/CD pipeline for automated builds  
✅ Multi-platform support (AMD64 & ARM64)  
✅ Docker Hub integration for image hosting  

---

## ⚙️ Prerequisites
Before you begin, ensure you have:
- [Docker](https://www.docker.com/get-started) installed
- [Python 3.7+](https://www.python.org/downloads/)
- [Docker Hub](https://hub.docker.com/) account
- [GitHub](https://github.com/) account

---

## 🚀 Quick Start (Local Development)

### 1. Clone the Repository
```bash
git clone https://github.com/Svadha29/test_automation.git
cd test_automation
```

### 2. Set Up a Virtual Environment (Optional but Recommended)
```bash
python -m venv venv
source venv/bin/activate  # Linux/Mac
.\venv\Scripts\activate   # Windows
```

### 3. Install Dependencies
```bash
pip install -r requirements.txt
```

### 4. Run FastAPI Locally
```bash
uvicorn main:app --reload
```
🔹 Access the API at: [http://localhost:8000](http://localhost:8000)  
🔹 Interactive API docs (Swagger UI): [http://localhost:8000/docs](http://localhost:8000/docs)  

---

## 🐳 Docker Deployment

### 1. Build the Docker Image
```bash
docker build -t fastapi-app .
```

### 2. Run the Container
#### For Apple Silicon (ARM64) Macs
```bash
docker run --platform linux/amd64 -d -p 8000:8000 fastapi-app
```
#### For AMD64 (Intel/AMD) Systems
```bash
docker run -d -p 8000:8000 fastapi-app
```
#### If Port 8000 is Already in Use
```bash
docker run -d -p 8001:8000 fastapi-app  # Now accessible at http://localhost:8001
```

### 3. Verify the Container is Running
```bash
docker ps
```
#### Expected Output:
```
CONTAINER ID   IMAGE         COMMAND                  PORTS                    NAMES
abc123def456   fastapi-app   "uvicorn main:app..."   0.0.0.0:8000->8000/tcp   awesome_fastapi
```

### 4. Check Logs (If Needed)
```bash
docker logs <container-id>
```

---

## 🔌 API Endpoints
| Endpoint        | Method | Description                |
|---------------|--------|----------------------------|
| `/`           | GET    | Returns a welcome message |
| `/items/{item_id}` | GET    | Returns the provided item_id |

#### Example Requests:
```bash
curl http://localhost:8000/
# Output: {"message": "Hello World"}

curl http://localhost:8000/items/42
# Output: {"item_id": 42}
```

---

## 🤖 CI/CD with GitHub Actions

The `.github/workflows/DockerBuild.yml` file automates:
- Building the Docker image on every git push
- Pushing the image to Docker Hub

### 🔑 Required GitHub Secrets
- **DOCKERHUB_USERNAME** → Your Docker Hub username
- **DOCKERHUB_TOKEN** → Docker Hub access token with Read & Write permissions

#### How to Set Up Secrets:
1. Go to GitHub Repo → Settings → Secrets → Actions
2. Click "New Repository Secret"
3. Add `DOCKERHUB_USERNAME` and `DOCKERHUB_TOKEN`

---

## 🛠 Troubleshooting

### ❌ Error: Port Already in Use
```bash
# Find the conflicting container
docker ps
docker stop <container-id>  # Stop it
```

### ❌ Error: Platform Mismatch (Apple Silicon)
```bash
docker run --platform linux/amd64 -d -p 8000:8000 fastapi-app
```

### ❌ Error: Docker Login Failed
Ensure your `DOCKERHUB_TOKEN` has Read & Write permissions.

---

## 📦 Docker Hub Integration
🔗 **Image URL:** [https://hub.docker.com/r/svadha29/test_automation](https://hub.docker.com/r/svadha29/test_automation)

#### Pull the Latest Image
```bash
docker pull svadha29/test_automation:latest
```

---

🚀 **Happy Coding!** 🎉

