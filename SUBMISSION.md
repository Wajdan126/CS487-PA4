<div align="center">

# PA4 Submission: TaskFlow Pipeline

<img alt="GitHub only" src="https://img.shields.io/badge/Submit-GitHub%20URL%20Only-10b981?style=for-the-badge">
<img alt="Total points" src="https://img.shields.io/badge/Total-100%20points-7c3aed?style=for-the-badge">

</div>

## Student Information

| Field | Value |
|---|---|
| Name | Wajdan Rasool |
| Roll Number | `27100319` |
| GitHub Repository URL | `https://github.com/Wajdan126/CS487-PA4` |
| Resource Group | `rg-sp26-27100319` |
| Assigned Region | `ukwest` |

## Evidence Rules

- All screenshots are stored under `docs/` and embedded using relative paths.
- Portal screenshots show resource names and Azure page context.
- CLI screenshots show command output where command-line verification was required.
- Secrets such as keys, passwords, and connection strings are masked where applicable.

---

## Task 1: App Service Web App (15 points)

### Evidence 1.1: Forked Repository

![Task 1 repository evidence](docs/task1-01.png)

Description: This screenshot shows the GitHub repository used for the PA4 work. It proves the project is stored in the required repository structure and can be submitted by GitHub URL.

### Evidence 1.2: App Service Overview

![Task 1 App Service overview](docs/task1-02.png)

Description: This screenshot shows the deployed Azure App Service for the TaskFlow web application. It identifies the running Web App resource in the assigned resource group and region.

### Evidence 1.3: Deployment Center / GitHub Actions

![Task 1 deployment evidence 1](docs/task1-03.png)

Description: This screenshot provides deployment evidence for the App Service. It shows that the web application deployment is connected to the repository workflow.

![Task 1 deployment evidence 2](docs/task1-04.png)

Description: This screenshot provides additional deployment evidence for the Web App. It confirms the deployment pipeline completed and the App Service received the web application build.

### Evidence 1.4: Live Web UI

![Task 1 live web UI](docs/task1-05.png)

Description: This screenshot showsApplication Settings configured.

---

## Task 2: Azure Container Registry (15 points)

### Evidence 2.1: ACR Overview

![Task 2 ACR overview](docs/task2-01.png)

Description: This screenshot shows the Azure Container Registry resource used for PA4. The registry stores the images used by AKS, ACI, and the Function App.

![ACR access keys page shows the admin user is enabled for image pulls.](docs/task2-02.png)

### Evidence 2.2: Docker Builds

![Task 2 Docker build evidence 1](docs/task2-03.png)

Description: This screenshot shows one of the Docker image build steps. It provides evidence that the container image was built before being pushed to ACR.

![Task 2 Docker build evidence 2](docs/task2-04.png)

Description: This screenshot shows another image build or tag step for the PA4 containers. It supports the required evidence that all pipeline services were containerized.

![Task 2 Docker build evidence 3](docs/task2-05.png)

Description: This screenshot provides build evidence for another PA4 image. The three images used in the assignment are `validate-api`, `report-job`, and `func-app`.

![Task 2 Docker build evidence 4](docs/task2-05.png)

Description: This screenshot documents another build or push command output. It helps show the image preparation workflow before Azure deployment.

![Task 2 Docker build evidence 5](docs/task2-06.png)

Description: This screenshot shows local test of the validator.

### Evidence 2.3: ACR Repositories

![Task 2 ACR repositories 1](docs/task2-07.png)

Description: This screenshot shows Validator image is tagged and pushed to ACR successfully.

![Task 2 ACR repositories 2](docs/task2-08.png)

Description: This screenshot shows Report-job image is tagged and pushed to ACR successfully

![Task 2 ACR repositories 3](docs/task2-09.png)

Description: This screenshot shows Function App image is tagged and pushed to ACR successfully

![Task 2 ACR repositories 4](docs/task2-10.png)

Description: This screenshot completes the ACR evidence for Task 2. It confirms the container registry contains the image artifacts needed by the pipeline.

---

## Task 3: Durable Function Implementation (12 points)

### Evidence 3.1: Completed Function Code

Completed file: [function_app.py](function-app/function_app.py)

Description: The Durable Function orchestrator gets the order input, calls `validate_activity`, rejects invalid orders, and calls `report_activity` for valid orders. The report activity creates an ACI report container and returns the generated Blob report URL.

![Task 3 function implementation 1](docs/task3-01.png)

Description: This screenshot shows func start shows the Durable Function handlers are registered.

![Task 3 function implementation 2](docs/task3-02.png)

Description: This screenshot shows Local smoke test starts the orchestrator and returns status query URLs

### Evidence 3.2: Local Function Handler Listing

![Task 3 function handler listing](docs/task3-03.png)

Description: This screenshot shows Repository changes are synced before rebuilding and deploying the Function App image.
---

## Task 4: Function App Container Deployment (8 points)

### Evidence 4.1: Function App Container Configuration

![Task 4 Function App container configuration 1](docs/task4-01.png)

Description: This screenshot shows  Updated Function App container image is rebuilt and pushed to ACR.

![Task 4 Function App container configuration 2](docs/task4-02.png)

Description: This screenshot Function App deployment configuration shows the ACR container image is selected.

### Evidence 4.2: Orchestration Smoke Test

![Task 4 orchestration smoke test 1](docs/task4-03.png)

Description: This screenshot shows  Function list shows http_starter, my_orchestrator, validate_activity, and report_activity.

![Task 4 orchestration smoke test 2](docs/task4-04.png)

Description: This screenshot shows Curl request starts the deployed orchestration and returns the instance/status URLs.

### Evidence 4.3: Expected Failed Status Before Downstream Wiring

![Task 4 expected status evidence](docs/task4-05.png)

Description: This screenshot shows Status query which shows the expected failure before downstream settings are complete.

---

## Task 5: AKS Validator (15 points)

### Evidence 5.1: AKS Cluster

![Task 5 AKS cluster](docs/task5-01.png)

Description: This screenshot shows kubectl get nodes confirms the AKS cluster node is running.

### Evidence 5.2: Kubernetes Nodes and Pods

![Task 5 Kubernetes nodes and pods](docs/task5-02.png)

Description: This screenshot shows kubectl get pods confirms the validator pod is running.

### Evidence 5.3: Kubernetes Service

![Task 5 Kubernetes service](docs/task5-03.png)

Description: This screenshot shows Kubernetes service shows the LoadBalancer external IP for the validator.
### Evidence 5.4: Validator API Tests

![Task 5 validator API tests](docs/task5-04.png)

Description: This screenshot shows validator API test evidence. It proves `/health` works and that `/validate` accepts valid orders and rejects orders where quantity exceeds the limit.

### Evidence 5.5: Function App `VALIDATE_URL` and Idle Behavior

![Task 5 Function App validator setting and idle evidence](docs/task5-05.png)

Description: This screenshot shows  Function App setting VALIDATE_URL points to the AKS validator endpoint.

---

## Task 6: ACI Report Job (15 points)

### Evidence 6.1: Blob Container

![Task 6 Blob container](docs/task6-01.png)

Description: This screenshot shows the Blob Storage container used for generated PDF reports. It proves the `reports` container exists as the report output destination.

### Evidence 6.2: Manual ACI Run

![Task 6 manual ACI run](docs/task6-02.png)

Description: This screenshot shows Manual ACI report test reaches Succeeded and uploads TEST-001.pdf.
### Evidence 6.3: ACI Logs

![Task 6 ACI logs](docs/task6-03.png)

Description: This screenshot shows Reports container shows the generated PDF file in Blob Storage.

### Evidence 6.4: Generated PDF

![Task 6 generated PDF evidence](docs/task6-03.png)

Description: This screenshot shows the generated PDF in Blob Storage or opened from the Blob URL. It proves the ACI report job wrote the report file successfully.

### Evidence 6.5: Function App Managed Identity and IAM

![Task 6 managed identity and IAM 1](docs/task6-04.png)

Description: This screenshot shows User-assigned managed identity mi-pa4-27100319 is attached to the Function App.


### Evidence 6.6: Report App Settings
![Function App settings show required report, ACR, and storage values.](docs/task6-05.png)
Description: Function App settings show required report, ACR, and storage values.

![Task 6 report app settings](docs/task6-06.png)

Description: This screenshot shows  Additional Function App settings are configured for the report job workflow.


---

## Task 7: End-to-End Pipeline (15 points)

### Evidence 7.1: Web App Wiring

![Task 7 Web App wiring 1](docs/task7-01.png)

Description: This screenshot shows  Web App settings connect the dashboard to the Function start and status endpoints.

![Task 7 Web App wiring 2](docs/task7-02.png)

Description: This screenshot shows Happy path order form is filled with a valid quantity before submission.

### Evidence 7.2: Happy Path UI

![Task 7 happy path UI 1](docs/task7-03.png)

Description: This screenshot shows Status panel which shows the valid order running with a live orchestration instance ID.
![Task 7 happy path UI 2](docs/task7-04.png)

Description: This screenshot shows which Status panel shows the valid order completed and displays the report link.


![Task 7 happy path UI 3](docs/task7-05.png)

Description: This screenshot shows  Storage command shows the generated PDF blob for the happy-path order.

![Azure Blob container shows the new PDF created for the order.](docs/task7-06.png)
Description: Azure Blob container shows the new PDF created for the order.

![Downloaded PDF file is available locally after the completed run.](docs/task7-07.png)
Description: Downloaded PDF file is available locally after the completed run.

![Generated PDF opens successfully and shows the order report](docs/task7-08.png)
Description: Generated PDF opens successfully and shows the order report

### Evidence 7.3: Backend Participation

![Task 7 backend evidence 1](docs/task7-09.png)

Description: This screenshot shows Function evidence which shows the orchestration and activities ran successfully

![Task 7 backend evidence 2](docs/task7-10.png)

Description: This screenshot shows AKS pod logs show the validator received /validate traffic during the run



### Evidence 7.4: Reject Path UI

![Task 7 reject path UI 1](docs/task7-11.png)

Description: This screenshot shows Reject path UI shows the invalid order was rejected with a clear reason.

![Task 7 reject path UI 2](docs/task7-12.png)

Description: This screenshot shows Function monitoring evidence shows the reject-path orchestration result.

![Task 7 reject path no ACI evidence](docs/task7-13.png)

Description: This screenshot shows Resource group overview shows the deployed Azure resources for the project.

![Resource group resources list shows App Service, Function App, ACR, Storage, and AKS.](docs/task7-14.png)
Description: Resource group resources list shows App Service, Function App, ACR, Storage, and AKS.

---

## Task 8: Write-up and Architecture Diagram (5 points)

### Evidence 8.1: Architecture Diagram

![TaskFlow architecture diagram](docs/Architecture_Diagram_Cloud_PA4.png)

Description: This architecture diagram shows the full TaskFlow pipeline, including GitHub CI/CD, Web App, Durable Function orchestration, AKS validator, ACI report job, Blob Storage, ACR image pulls, and managed identity permissions.


### Question 8.2: Service Selection

**App Service**

Azure App Service was used for the web dashboard because it is a good choice for hosting a normal web application. The user opens this web app in the browser and submits an order from there. App Service also connects easily with GitHub, so the app can be deployed through CI/CD after pushing code. It is also easier than running the web app manually on a virtual machine because Azure manages the hosting, HTTPS, and runtime environment.

**Durable Functions**

Durable Functions was used for the orchestration part of the pipeline. The order process has more than one step, so it should not be handled by one simple HTTP request only. The Durable Function first calls the validator service, then decides whether to reject the order or start the report job. It also stores the workflow state, so the web app can keep checking the status later.

**Azure Kubernetes Service (AKS)**

AKS was used for the validator API because the validator is a long-running service. It needs a stable endpoint because the Function App calls it every time an order is submitted. AKS is more complex than ACI, but it gives more control over deployments, pods, services, and load balancing. In this project, the validator runs as a Kubernetes deployment and is exposed through a LoadBalancer service.

**Azure Container Instance (ACI)**

ACI was used for the report job because the report generator is a short-lived task. It only needs to start, generate the PDF, upload it to Blob Storage, and then stop. This is a better fit for ACI because we do not need to keep a container running all the time. It also saves cost because the container is used only when a report is needed.

**Azure Container Registry (ACR)**

ACR was used as the central place to store all container images. The validator image, report-job image, and function-app image were all pushed to ACR. After that, AKS, ACI, and the Function App could pull their required images from the same registry. This keeps the image management clean and simple.

### Question 8.3: ACI vs AKS

AKS and ACI behaved differently in this assignment. AKS kept running even when there were no orders being submitted. This is because the validator service is a long-running service and the AKS node still exists even when it is idle. So, even after 10 minutes of no traffic, the AKS cluster is still available and can receive new validation requests.

ACI is different. In this pipeline, ACI is only created when a valid order needs a report. After the report job finishes, the container exits. So for ACI, "idle" does not really mean a running service waiting for requests. It means no report container is running because there is no report job at that time.

If a malicious user pressed the Submit button 1000 times in one minute, the report side could become expensive if many valid orders created many ACI jobs. Each valid order can create a new container instance. The AKS node is already running, so extra validator requests mainly add traffic and load to the same running service. The bigger cost risk is from many valid orders creating many short-lived ACI containers and many PDF files.

### Question 8.4: Durable Functions vs Plain HTTP

A normal HTTP function is not the best choice for this workflow because the process has multiple steps. The report step can take some time, and a normal HTTP request may timeout or become hard to track. Durable Functions solves this by saving the workflow state and giving a status URL that the web app can poll.

It also makes the logic easier to manage. The orchestrator can call the validator first and then decide what to do next. If the order is invalid, it stops early and returns a rejected status. If the order is valid, it starts the report activity. This is cleaner than using two separate HTTP functions that call each other manually.

Durable Functions also helps with failure handling. If one step fails, the workflow history is still available. This makes debugging easier because I can see which activity failed and why.

### Question 8.5: Cost Review

![Task 8 Cost Management screenshot](docs/task8-cost.png)

The Cost Management screenshot above shows the cost for my resource group `rg-sp26-27100319`. The total cost for this programming assignment was small because I used the required low-cost resources. I used the Basic ACR, B1 App Service plan, one AKS node, and short-lived ACI containers.

The most expensive resource was the AKS cluster. This is expected because the AKS node keeps running even when no order is being submitted. ACI only runs for a short time during the report job, so it does not stay active all the time. This shows why AKS is good for a stable service, but ACI is better for short jobs.

### Question 8.6: Challenges Faced

One issue I faced was setting the correct environment variables in the Function App. The orchestrator needs values like `VALIDATE_URL`, `REPORT_IMAGE`, `ACR_SERVER`, `ACR_USERNAME`, `STORAGE_ACCOUNT_URL`, and the managed identity client ID. If one setting is missing or wrong, the pipeline can start but fail later. I debugged this by checking the Function App application settings and then testing the orchestration status URL.

Another issue was making sure the Function App could reach the validator running on AKS. The validator service needed an external IP from the Kubernetes LoadBalancer. At first, the service IP was not immediately ready. I used `kubectl get service` and waited until the external IP appeared. Then I tested `/health` and `/validate` with curl before adding the URL to the Function App settings.

I also had to check that the report job actually uploaded the PDF to Blob Storage. The ACI logs helped confirm that the report job ran successfully. After that, I checked the `reports` blob container and verified that the PDF file with my order ID was created.

---
