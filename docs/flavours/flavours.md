---
description: "EasyTask deployment models — compare Cloud vs On-Premises deployments. Choose the right model for your enterprise workflow orchestration needs."
keywords: "EasyTask deployment, cloud deployment, on-premises deployment, enterprise scheduling, hybrid deployment, workflow orchestration hosting"
---

# 🌍 Deployment Models

EasyTask provides flexible deployment models to meet diverse business needs — from startups to large enterprises. Whether you need the flexibility of the cloud or the control of an on-premises setup, EasyTask adapts to fit your operational and security requirements.

---

## ⚖️ Model Comparison

| Feature | ☁️ Cloud | 🏢 On-Premises |
|---------|:-----------------------|:---------------------------------------|
| **Setup** | Fully managed, quick start | Self-hosted on your infrastructure |
| **Scalability** | Automatic, on-demand | Manual scaling via additional hosts |
| **Data Location** | EasyTask-managed cloud | Your data centers, full data sovereignty |
| **Security Control** | Shared responsibility | Full control over security policies |
| **Upkeep** | Managed by EasyTask | Your team manages updates and patches |
| **Compliance** | Standard certifications | Custom compliance configurations |
| **Best For** | Dynamic workloads, remote teams, fast time-to-value | Regulated industries, strict data policies, custom infrastructure |

---

## ☁️ Cloud

The cloud deployment model offers flexibility and scalability, allowing you to run tasks and services in a fully managed remote environment. This option is ideal for businesses with dynamic workloads, remote teams, or global operations.

**Key Benefits:**
- 📈 Scalable and flexible to meet demand
- 🌐 Accessible from anywhere
- 💲 Cost-efficient with pay-as-you-go pricing
- ☁️ Integrates with modern cloud services

---

## 🏢 On-Premises

The on-premises model gives you maximum control over infrastructure, hardware, and data. It's well-suited for organizations with strict compliance, regulatory, or security requirements and ensures everything runs within your own data centers.

**Key Benefits:**
- 🔒 Full control over infrastructure and data
- 🛡️ Customizable security and compliance policies
- 🚫 No dependency on external providers
- 📍 Ensures data sovereignty and local compliance

---

## 🧭 Choosing the Right Model

Use this guide to select the deployment model that fits your organization:

**Choose Cloud if you:**
- Need to get started quickly without managing infrastructure
- Have distributed teams that need remote access
- Want automatic scaling for variable workloads
- Prefer predictable operational expenses

**Choose On-Premises if you:**
- Operate in a regulated industry (finance, healthcare, pharma, government)
- Require data to stay within specific geographic boundaries
- Need custom security policies or network configurations
- Have existing infrastructure and prefer capital expenditure

> 💡 Both models deliver the full EasyTask feature set including 40+ integrations, real-time monitoring, adhoc commands, and the AI support chatbot. The feature set is identical — only the hosting location and management responsibility differ.

---

## ❓ Frequently Asked Questions

### Can I switch from Cloud to On-Premises (or vice versa) later?
Yes. EasyTask's architecture is deployment-agnostic. Your task definitions, configurations, and integrations can be migrated between deployment models. Contact support for assistance with migration planning.

### Does the Cloud model support custom integrations?
Yes. The cloud deployment includes the same integration server capabilities as on-premises. All 40+ pre-built integrations and custom webhook integrations are available in both models.

### What networking requirements does the On-Premises model have?
On-Premises deployments require network connectivity between the scheduler, agents, and integration server components. The scheduler communicates with agents via an internal message broker (RabbitMQ). Port 10001 must be open for the Podman API. Specific networking details are covered in the installation guide.

---

## ➡️ Next Steps

- [Installation Guide](../getting_started/installation/pre_req.md) — system requirements and setup
- [Architecture Overview](../architecture/architecture_intro.md) — understand EasyTask's components
- [Getting Started](../getting_started/getting_started_intro.md) — deploy your first EasyTask instance
- [Integrations](../integrations/integrations_intro.md) — explore 40+ pre-built connectors
