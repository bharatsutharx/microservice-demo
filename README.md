<!-- <p align="center">
<img src="/src/frontend/static/icons/Hipster_HeroLogoMaroon.svg" width="300" alt="Online Boutique" />
</p> -->


**Online Boutique** is a cloud-first microservices demo application.  The application is a
web-based e-commerce app where users can browse items, add them to the cart, and purchase them.


If you’re using this demo, please **★Star** this repository to show your interest!


**This project serves as a hands-on industry-level DevOps implementation, covering the entire DevOps lifecycle, from containerization to CI/CD, Kubernetes, Infrastructure as Code (IaC), monitoring, and GitOps.**

I cloned source code from originally Google Cloud repo, and this is tightly coupled with gcp dependencies so i modified to remove GCP-specific dependencies and is now fully containerized for local and cloud-based deployment.

## DevOps Workflow Implementation Plan:

![DevOps Workflow](/docs/img/Arch_micro.png)

* **Dockerization** – Each service is containerized with optimized Dockerfiles and Docker Compose.

* **CI/CD using Jenkins** – Automate build, test, and deployment pipelines.

* **Kubernetes Manifests** – Define K8s deployment configurations for all microservices.

* **Infrastructure as Code (IaC)** – Use Terraform to provision cloud resources.

* **GitOps with ArgoCD** – Automate Kubernetes deployments using Git-based workflows.

* **Monitoring & Logging** – Implement observability using Prometheus, Grafana, and Loki.

* **Advanced Microservices Management** – Optimize networking, security, and scaling for production readiness.

## Architecture

**Online Boutique** is composed of 11 microservices written in different
languages that talk to each other over gRPC.

![Architecture of microservices](/docs/img/Struc-Micro.png)


| Service                                              | Language      | Description                                                                                                                       |
| ---------------------------------------------------- | ------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| [frontend](/src/frontend)                           | Go            | Exposes an HTTP server to serve the website. Does not require signup/login and generates session IDs for all users automatically. |
| [cartservice](/src/cartservice)                     | C#            | Stores the items in the user's shopping cart in Redis and retrieves it.                                                           |
| [productcatalogservice](/src/productcatalogservice) | Go            | Provides the list of products from a JSON file and ability to search products and get individual products.                        |
| [currencyservice](/src/currencyservice)             | Node.js       | Converts one money amount to another currency. Uses real values fetched from European Central Bank. It's the highest QPS service. |
| [paymentservice](/src/paymentservice)               | Node.js       | Charges the given credit card info (mock) with the given amount and returns a transaction ID.                                     |
| [shippingservice](/src/shippingservice)             | Go            | Gives shipping cost estimates based on the shopping cart. Ships items to the given address (mock)                                 |
| [emailservice](/src/emailservice)                   | Python        | Sends users an order confirmation email (mock).                                                                                   |
| [checkoutservice](/src/checkoutservice)             | Go            | Retrieves user cart, prepares order and orchestrates the payment, shipping and the email notification.                            |
| [recommendationservice](/src/recommendationservice) | Python        | Recommends other products based on what's given in the cart.                                                                      |
| [adservice](/src/adservice)                         | Java          | Provides text ads based on given context words.                                                                                   |
| [loadgenerator](/src/loadgenerator)                 | Python/Locust | Continuously sends requests imitating realistic user shopping flows to the frontend.                                              |

## Screenshots

| Home Page                                                                                                         | Checkout Screen                                                                                                    |
| ----------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| [![Screenshot of store homepage](/docs/img/online-boutique-frontend-1.png)](/docs/img/online-boutique-frontend-1.png) | [![Screenshot of checkout screen](/docs/img/online-boutique-frontend-2.png)](/docs/img/online-boutique-frontend-2.png) |
