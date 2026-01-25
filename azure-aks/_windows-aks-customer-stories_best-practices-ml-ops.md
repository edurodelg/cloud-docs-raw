---
merged_at: 2026-01-25T12:25:33.868057
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: windows-aks-customer-stories.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/windows-aks-customer-stories -->

# Windows AKS customer stories

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Explore how various industries are using Windows Containers on Azure Kubernetes Service (AKS) for seamless Kubernetes integration with minimal code modifications.

Learn directly from the customer stories listed here.

## Customer stories

### Finastra

LaserPro document management software is key to the Finastra vision of delivering the future of banking. Migrating from an on-premises management system to a cloud-based infrastructure using Windows containers on Azure Kubernetes Service has significantly increased agility through biweekly updates and reduced support costs for both customers and developers.

For more information visit [Finastra's Windows AKS customer story](https://customers.microsoft.com/en-us/story/1759082810297807726-finastra-azure-kubernetes-service-professional-services-en-united-kingdom).

### Relativity

Relativity, transitioned from virtual machines to Windows containers on Azure Kubernetes Service (AKS) to modernize its Windows code base, streamline development, and improve scalability.

This shift enabled faster, more cost-effective deployment of their products and services without rewriting millions of lines of code. The transition to a containerized architecture significantly reduced deployment cycles from six months to a single day, enhancing the speed and flexibility of Relativity’s engineering teams and leading to better performance and security in their application delivery.

For more information visit [Relativity’s Windows AKS customer story](https://customers.microsoft.com/story/1516554049543037694-windows-containers-helps-relativity-boost-reliability-security).

### Duck Creek

Duck Creek Technologies modernized its insurance software solutions by adopting Windows containers on Azure Kubernetes Service (AKS), significantly enhancing operational efficiency and reducing time to market for new features. This transition to AKS enabled Duck Creek to offer scalable, reliable, and up-to-date SaaS solutions to its insurance clients, supporting rapid deployment and active delivery of updates.

By containerizing their applications to Windows Containers, Duck Creek could maintain the flexibility and robustness of their products without extensive code rewriting, thereby ensuring high availability and scalability, especially critical during peak demand periods like natural disasters. This move represents Duck Creek's commitment to leveraging cutting-edge technology for Insurtech innovation.

### Forza

Forza Horizon 5, developed by Turn 10 Studios, achieved remarkable performance and scalability by transitioning to Azure Kubernetes Service (AKS) with Windows-based containers. This shift allowed the team to adapt swiftly to demand spikes, handling over 10 million concurrent players at launch, the biggest first week in Xbox Game Studios history.

By utilizing Windows AKS, they were able to significantly reduce infrastructure management tasks, enhancing both the development process and the gaming experience. The move to containerized architecture enabled rapid scaling from 600,000 to 3 million concurrent users and reduced infrastructure costs, demonstrating the effectiveness of AKS in high-demand, low-latency environments like gaming.

For more information visit [Forza Horizon 5 runs on Windows containers on Azure Kubernetes Services](https://techcommunity.microsoft.com/blog/itopstalkblog/forza-horizon-5-runs-on-windows-containers-on-azure-kubernetes-services/3570404).

### Microsoft Experience + Devices

Microsoft's E+D group, responsible for supporting products such as Teams and Office modernized the Microsoft 365 infrastructure by transitioning to Windows containers on Azure Kubernetes Service (AKS), aiming for more consistent, efficient DevOps within strict security and compliance frameworks.

The transition enabled Microsoft 365 developers to focus more on innovation and iterating quickly, leveraging the benefits of AKS like security-optimized hosting, automated compliance checks, and centralized capacity management, thereby accelerating development while optimizing resource utilization and costs.


---

<!-- DOCUMENTO FUSIONADO: best-practices-ml-ops.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/best-practices-ml-ops -->

# Machine learning operations (MLOps) best practices in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes best practices and considerations to keep in mind when using MLOps in AKS. For more information on MLOps, see [Machine learning operations (MLOps) for AI and machine learning workflows](concepts-machine-learning-ops).

## Infrastructure as code (IaC)

[IaC](/en-us/devops/deliver/what-is-infrastructure-as-code) enables consistent and reproducible infrastructure provisioning and management for a range of application types. With intelligent application deployments, your IaC implementation might change throughout the AI pipeline, as the compute power and resources needed for inferencing, serving, training, and fine-tuning models can vary. Defining and versioning IaC templates for your AI developer teams can help ensure consistency and cost-effectiveness across job types while demystifying their individual hardware requirements and accelerating the deployment process.

## Containerization

Managing your model weights, metadata, and configurations in container images allows for portability, simplified versioning, and reduced storage costs over time. With containerization, you can:

- Leverage existing container images, especially for large language models (LLMs) ranging in millions to billions of parameters in size and stable diffusion models, stored in secure container registries.
- Avoid single point of failure (SPOF) in your pipeline with the use of multiple lightweight containers containing the unique dependencies for each task instead of maintaining one large image.
- Store large text/image datasets outside of your base container image and reference them when needed at runtime.

[Get started with the Kubernetes AI Toolchain Operator](ai-toolchain-operator) to deploy a high performance LLM on AKS in a matter of minutes.

## Model management and versioning

Model management and versioning are essential for tracking changes to your models over time. By versioning your models, you can:

- Maintain consistency across your model containers for ease of deployment in different environments.
- Employ parameter-efficient fine-tuning (PEFT) methods to iterate faster on a subset of model weights and maintain new versions in lightweight containers.

## Automation

Automation is key to reducing manual errors, increasing efficiency, and ensuring consistency across the ML lifecycle. By automating tasks, you can:

- Integrate alerting tools to automatically trigger a vector ingestion flow as new data flows into your application.
- Set model performance thresholds to track degradations and trigger retraining pipelines.

## Scalability and resource management

Scalability and resource management are critical for ensuring that your AI pipeline can handle the demands of your application. By optimizing your resource usage, you can:

- Integrate tools that efficiently use your allocated CPU, GPU, and memory resources through distributed computing and multiple levels of parallelism (for example: data, model, and pipeline parallelism).
- Enable autoscaling on your compute resources to support high model request volumes at peak times and scale down in off-peak hours.
- Similar to your traditional applications, plan for disaster recovery by following
[AKS resiliency and reliability best practices](ha-dr-overview).

## Security and compliance

Security and compliance are critical for protecting your data and ensuring that your AI pipeline meets regulatory requirements. By implementing security and compliance best practices, you can:

- Integrate common vulnerability and exposure (CVE) scanning to detect common vulnerabilities on open-source model container images.
- Use
[Microsoft Defender for Containers](/en-us/azure/defender-for-cloud/defender-for-containers-introduction)for model container images stored in your Azure Container Registry.

- Use
- Maintain an audit trail of the ingested data, model changes, and metrics to remain compliant with your organizational policies.

## Next steps

Learn about best practices across other areas of your application deployment and operations on AKS:
