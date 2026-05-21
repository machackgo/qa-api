# QA-API: Docker & GitHub Actions CI/CD Deployment

## 1. Project Overview

QA-API is a containerized backend API deployment scaffold built as part of MLOps course deployment work. This project demonstrates infrastructure automation with Docker containerization, automated CI/CD via GitHub Actions, and VM-based deployment orchestration. The backend is designed as a deployment template showing modern DevOps practices for containerized services.

## 2. Problem Solved

This project addresses several MLOps infrastructure and deployment challenges:
- Need for containerized, reproducible API service deployments
- - Requirement for automated CI/CD pipelines that trigger on code changes
  - - Desire to demonstrate Docker containerization best practices
    - - Need for infrastructure reproducibility across development and production
      - - Integration of frontend and backend services with coordinated deployment
       
        - ## 3. Deployment Workflow
       
        - The system follows a containerization-to-deployment architecture:
       
        - ```
          Code Push to Main Branch
              ↓
          GitHub Actions Trigger
          (deploy.yml workflow)
              ↓
          Docker Image Build
          (backend & frontend Dockerfiles)
              ↓
          SSH Authentication
          (GitHub Secrets: SSH key)
              ↓
          VM Deployment
          (automated Docker container orchestration)
              ↓
          Port Mapping & Service Runtime
          (backend 22014:9004, frontend 22004:7004)
          ```

          ## 4. Tech Stack

          - **Containerization**: Docker with Python 3.11-slim base images
          - - **API Server**: Uvicorn ASGI server
            - - **CI/CD Pipeline**: GitHub Actions with automated deployment workflows
              - - **Deployment Target**: Virtual Machine with SSH access
                - - **Container Orchestration**: Docker daemon with port mapping
                  - - **Backend Service**: Port 9004 (container) mapped to 22014 (host VM)
                    - - **Frontend Service**: Port 7004 (container) mapped to 22004 (host VM)
                     
                      - ## 5. Key Features
                     
                      - - **Docker Containerization**: Complete containerization of backend service using Python 3.11-slim base image with optimized layer caching
                        - - **Uvicorn ASGI Server**: High-performance ASGI server deployment configured in Dockerfile
                          - - **Automated GitHub Actions CI/CD**: Workflow triggers on main branch pushes with Docker build and deployment automation
                            - - **Infrastructure Automation**: Complete deployment pipeline from code to running container via GitHub Actions
                              - - **Port Mapping Strategy**: Sophisticated port mapping for multiple services on single VM host
                                - - **Frontend Integration**: Coordinated deployment of frontend and backend services
                                  - - **Secure Credential Management**: GitHub Secrets integration for sensitive deployment information
                                    - - **Container Lifecycle Management**: Automated cleanup of old containers before new deployments
                                     
                                      - ## 6. How to Run Locally
                                     
                                      - ### Prerequisites
                                      - - Python 3.11 or later
                                        - - Docker (for containerized deployment)
                                          - - Git
                                           
                                            - ### Local Development Setup
                                           
                                            - 1. Clone the repository:
                                              2.    ```bash
                                                       git clone https://github.com/machackgo/qa-api.git
                                                       cd qa-api
                                                       ```

                                                    2. Install dependencies:
                                                    3.    ```bash
                                                             pip install -r requirements.txt
                                                             ```

                                                          3. Run the backend service locally:
                                                          4.    ```bash
                                                                   uvicorn main:app --host 0.0.0.0 --port 9004
                                                                   ```

                                                                The service will be available at `http://localhost:9004`

                                                            ## 7. How to Run with Docker

                                                      ### Build Backend Docker Image

                                                ```bash
                                                docker build -f backend/Dockerfile -t qa-api-backend .
                                                ```

                                                ### Run Backend Container

                                              ```bash
                                              docker run -d --name qa-api-backend -p 9004:9004 qa-api-backend
                                              ```

                                              ### For Frontend Service

                                              ```bash
                                              docker build -f frontend/Dockerfile -t qa-api-frontend .
                                              docker run -d --name qa-api-frontend -p 7004:7004 qa-api-frontend
                                              ```

                                              ## 8. Skills Demonstrated

                                              This project showcases several professional DevOps and infrastructure engineering competencies:

                                              - **Docker & Container Engineering**: Building optimized Docker images with efficient base image selection (slim variants), layer caching, and multi-service coordination
                                              - - **GitHub Actions CI/CD**: Designing and implementing automated workflows that trigger on code changes with proper pipeline stages
                                                - - **Infrastructure Automation**: Complete automation of deployment pipeline from code push through container orchestration
                                                  - - **SSH-Based Deployment**: Secure remote deployment using SSH credentials management via GitHub Secrets
                                                    - - **Port Mapping & Networking**: Understanding of container networking, port binding, and host-container communication
                                                      - - **Container Orchestration Basics**: Docker daemon management, container lifecycle (build, run, stop, remove), and service coordination
                                                        - - **Reproducible Deployments**: Creating deployment pipelines that produce consistent results across environments
                                                         
                                                          - ## 9. VeriBridge Proof Evidence
                                                         
                                                          - All infrastructure claims are directly verifiable in repository files:
                                                         
                                                          - | Infrastructure Component | Evidence Location | Proof Details |
                                                          - |-------------------------|-------------------|----------------|
                                                          - | Docker containerization - backend | `backend/Dockerfile` | Complete Dockerfile with build stages |
                                                          - | Docker containerization - frontend | `frontend/Dockerfile` | Complete Dockerfile for frontend service |
                                                          - | Python 3.11-slim base image | `backend/Dockerfile` line 1 | `FROM python3.11-slim` |
                                                          - | Uvicorn ASGI server configuration | `backend/Dockerfile` line 12 | `CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "9004"]` |
                                                          - | Dependency installation | `backend/Dockerfile` lines 5-6 | `COPY requirements.txt` and `RUN pip install` |
                                                          - | GitHub Actions CI/CD pipeline | `.github/workflows/deploy.yml` | Complete deployment automation workflow |
                                                          - | Automated trigger on main branch | `.github/workflows/deploy.yml` line 4 | `on: push: branches: - main` |
                                                          - | Docker build automation | `.github/workflows/deploy.yml` line 33 | `docker build -f backend/Dockerfile -t qa-api-backend .` |
                                                          - | SSH-based VM deployment | `.github/workflows/deploy.yml` lines 16-37 | Complete SSH deployment automation with container orchestration |
                                                          - | GitHub Secrets integration | `.github/workflows/deploy.yml` lines 19, 21, 25 | Uses `secrets.VM_SSH_KEY`, `secrets.VM_HOST`, `secrets.VM_USER`, `secrets.VM_PORT` |
                                                          - | Backend port mapping | `.github/workflows/deploy.yml` line 36 | `docker run -d -p 22014:9004 qa-api-backend` |
                                                          - | Frontend port mapping | `.github/workflows/deploy.yml` line 37 | `docker run -d -p 22004:7004 qa-api-frontend` |
                                                          - | Container cleanup automation | `.github/workflows/deploy.yml` lines 30-31 | `docker stop` and `docker rm` commands |
                                                         
                                                          - ## 10. Recruiter Value & Skills
                                                         
                                                          - This project demonstrates valuable infrastructure and DevOps capabilities:
                                                         
                                                          - **Container Engineering**: Shows hands-on expertise in Docker image creation, optimization, and multi-service container management.
                                                         
                                                          - **CI/CD Automation**: Demonstrates ability to design and implement automated deployment pipelines that eliminate manual deployment steps and reduce errors.
                                                         
                                                          - **Infrastructure as Code**: Shows proficiency in defining infrastructure through code (GitHub Actions YAML), enabling reproducible and version-controlled deployments.
                                                         
                                                          - **Cloud/VM Deployment**: Demonstrates SSH-based remote deployment patterns used extensively in cloud and on-premise infrastructure management.
                                                         
                                                          - **DevOps Mindset**: Shows understanding of deployment automation, infrastructure reproducibility, and secure credential management principles.
                                                         
                                                          - **MLOps Context**: Portfolio project from MLOps course demonstrating practical deployment skills relevant to production machine learning systems.
                                                         
                                                          - ## 11. Future Improvements
                                                         
                                                          - - **Health Check Endpoints**: Add `/health` and `/readiness` endpoints for monitoring and orchestration
                                                            - - **Logging & Observability**: Integrate centralized logging and metrics collection for production monitoring
                                                              - - **API Documentation**: Add OpenAPI/Swagger documentation once API endpoints are implemented
                                                                - - **Testing & Validation**: Implement automated testing in CI/CD pipeline
                                                                  - - **Environment Management**: Support dev/staging/prod environment configurations
                                                                    - - **Container Registry**: Push images to Docker Hub or GitHub Container Registry
                                                                      - - **Kubernetes Migration**: Migrate to Kubernetes for production-grade container orchestration
                                                                        - - **Database Layer**: Add persistent data storage when needed
                                                                          - - **Load Balancing**: Add load balancer (nginx) for high availability
                                                                           
                                                                            - ---

                                                                            ## Repository Metadata

                                                                            **Suggested GitHub Description:**
                                                                            "Docker and GitHub Actions CI/CD deployment scaffold for containerized backend services. Demonstrates automated infrastructure deployment from MLOps course."

                                                                            **Suggested GitHub Topics:**
                                                                            - `docker`
                                                                            - - `github-actions`
                                                                              - - `ci-cd`
                                                                                - - `devops`
                                                                                  - - `mlops`
                                                                                    - - `deployment`
                                                                                      - - `containerization`
                                                                                        - - `infrastructure-automation`
                                                                                          - 
