\# DVWA Deployment on Kubernetes



\## 1. Project Overview



This project demonstrates the deployment of Damn Vulnerable Web Application

(DVWA) on a local Kubernetes cluster using Minikube.



The objective is to deploy DVWA and its database, access the application

locally, and demonstrate three web application vulnerabilities.



\## 2. Tools and Technologies



\- Kubernetes

\- Minikube

\- Docker Desktop

\- kubectl

\- DVWA

\- MariaDB

\- YAML

\- PowerShell



\## 3. Architecture



The project uses a local Minikube Kubernetes cluster.



Components:

\- DVWA Deployment: Runs the vulnerable web application.

\- DVWA Service: Provides access to DVWA inside the cluster.

\- MariaDB Deployment: Stores application data.

\- Database Service: Connects DVWA to MariaDB.

\- Namespace: Resources are organized in the dvwa namespace.

\- Port forwarding: Makes DVWA accessible through localhost.



\## 4. Deployment Steps



Create the namespace:



&#x20;   kubectl create namespace dvwa



Deploy the resources:



&#x20;   kubectl apply -f dvwa.yaml



Check the Kubernetes node:



&#x20;   kubectl get nodes



Check the pods:



&#x20;   kubectl get pods -n dvwa



Check the services:



&#x20;   kubectl get services -n dvwa



Access DVWA using port forwarding:



&#x20;   kubectl port-forward service/dvwa 8081:80 -n dvwa



Open in your browser:



&#x20;   http://localhost:8081



\## 5. Vulnerability Demonstrations



\### Attack 1: SQL Injection



Normal input:



&#x20;   1



Test input:



&#x20;   1' OR '1'='1' #



Observed result:

Multiple database records were returned instead of only the expected record.



Mitigation:

Use parameterized SQL queries and prepared statements.



\### Attack 2: Reflected Cross-Site Scripting (XSS)



Normal input:



&#x20;   Fayaz



Test input:



&#x20;   <script>alert('XSS')</script>



Observed result:

A browser alert displayed XSS.



Mitigation:

Use context-aware output encoding and safely handle untrusted input.



\### Attack 3: OS Command Injection



Normal input:



&#x20;   127.0.0.1



Test input:



&#x20;   127.0.0.1; whoami



Observed result:

\[Replace this line with the actual result you observed.]



Mitigation:

Avoid unsafe shell execution, validate input using strict allowlists,

and run applications with least privilege.



\## 6. Security Considerations



DVWA is intentionally vulnerable and is used for educational testing.



The application is accessed locally through Kubernetes port forwarding.

It should not be exposed publicly.



The database credentials are for demonstration purposes only.



\## 7. Conclusion



This project demonstrates deploying DVWA and MariaDB on Kubernetes,

verifying the deployment, and testing SQL Injection, Reflected XSS,

and OS Command Injection.



The demonstrations highlight the importance of secure coding,

input validation, output encoding, and least-privilege access.

