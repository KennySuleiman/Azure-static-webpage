# Azure-static-webpage
Creating a static website using Azure cloud service
# 🌐 Azure-Hosted Personal Portfolio Website

A modern, high-performance static portfolio website hosted entirely serverless on **Microsoft Azure**. This project leverages Azure Blob Storage for cost-effective static site hosting and integrates Azure CDN to ensure global low-latency delivery, custom domain mapping, and automated SSL/TLS encryption.

Built as part of an exploration into cloud infrastructure, this architecture eliminates the overhead of managing virtual machines or traditional web servers, resulting in a resilient, auto-scaling, and secure web presence costing mere fractions of a cent per month.

---

## 🏗️ Architecture Overview

The project utilizes a pure serverless cloud-native architecture:

### Core Components
* **Azure Storage Account (Blob Storage):** Acts as the origin server. The "Static Website Hosting" feature is enabled to serve assets directly from a specialized `$web` container.
* **Azure CDN (Standard Microsoft):** Caches asset deployments across global edge servers to minimize Time to First Byte (TTFB), while provisioning automated HTTPS certificates.
* **Resource Management:** All components are isolated within a dedicated Azure Resource Group (`portfolio-rg`) for clean lifecycle management.

---

## 🚀 Step-by-Step Deployment Guide

### Prerequisites
* An active **Azure Account** (Free Tier or Paid).
* A portfolio codebase (HTML5, CSS3, modern JavaScript). A basic fallback `index.html` is provided in the repository.

### Phase 1: Storage Infrastructure Provisioning
1. Log in to the [Azure Portal](https://portal.azure.com/).
2. Search for and select **Storage accounts**, then click **+ Create**.
3. Configure the **Basics** tab with the following architectural specifications:
    * **Subscription:** Choose your active subscription (e.g., *Free Trial*).
    * **Resource Group:** Click *Create new* and enter `portfolio-rg`.
    * **Storage account name:** Enter a globally unique, lowercase alphanumeric identifier (e.g., `yournameportfolio`).
    * **Region:** Select the geographical region nearest to your target audience (e.g., *East US*).
    * **Performance:** Select **Standard**.
    * **Redundancy:** Select **Locally-redundant storage (LRS)** to optimize cost-efficiency for static assets.
4. Click **Review + create**, and select **Create** once validation passes.

### Phase 2: Enabling Static Web Server Engine
1. Navigate to the newly deployed Storage Account resource.
2. In the left navigation menu under **Data management**, select **Static website**.
3. Toggle the state configuration to **Enabled**.
4. Configure the routing document mapping:
    * **Index document name:** `index.html`
    * **Error document path:** `404.html` *(optional)*
5. Click **Save**.
6. **Important:** Copy the generated **Primary endpoint** URL. This is the direct public HTTP route to your storage origin.

### Phase 3: Codebase Deployment
1. Under the *Static website* configuration panel, click the **$web** container link at the top.
2. Click **Upload**.
3. Drag and drop your frontend deployment bundle (`index.html`, style sheets, script files, media assets) into the context panel.
4. Expand the **Advanced** tab if necessary to verify standard blob access settings, then click **Upload**.
5. Test the live site by pasting the copied *Primary endpoint* URL into any web browser.

### Phase 4: CDN Integration & Secure HTTPS (Optional)
1. Within your Storage Account navigation menu, locate **Security + networking** and select **Azure CDN**.
2. Provision a new CDN profile:
    * **CDN profile option:** Create new.
    * **Pricing tier:** *Standard Microsoft* (Free credit eligible).
    * **CDN endpoint name:** Enter a unique endpoint name.
    * **Origin hostname:** Select or paste your Static Website *Primary endpoint* URL (omit the protocol prefix `http://`).
3. Click **Create**. Once provisioning completes, access your asset bundle via the accelerated, secure CDN endpoint URL (`https://yourname.azureedge.net`).

---

## 📈 Performance & Cost Optimization Best Practices

* **Cost Management Framework:** Always navigate to **Cost Management + Billing** in the portal to establish a budget threshold alert (e.g., $5.00) to protect against accidental usage outside free tiers.
* **Cache Invalidation:** When modifying codebase files (like updating an image or editing CSS), remember to purge your Azure CDN cache profile so edge locations pull the newest variations instantly.
* **Zero-Footprint Deletion:** To completely tear down this infrastructure and stop tracking telemetry/storage metrics, simply run:
    ```bash
    az group delete --name portfolio-rg --yes --no-wait
    ```

---

## 🛠️ Built With
* **Microsoft Azure Storage:** High-scale Object storage optimization.
* **Azure CDN:** Edge-caching framework for global performance delivery.
* **HTML5 / CSS3 / JavaScript:** Frontend presentation layers.



* An active **Azure Account** (Free Tier or Paid).
* A portfolio codebase (HTML5, CSS3, modern JavaScript). A basic fallback `index.html` is provided in the repository.
