# PRISMA CLOUD VISIBILITY AND CONTROL BOOTCAMP


### Lab Introduction

Thank you for joining today’s Visibility and Control camp. The lab will focus on the ways
that Prisma Cloud can help you secure cloud assets through posture and compliance tools.

Before we begin the lab let's start with a brief overview of the scenario to help frame the
context.

### Scenario

The Exampli Corp, a mock corporation, is rushing to finish a banking app for
their customer Bank of Anthos in time before the fiscal year ends.
Up against challenging deadlines, the development and infrastructure teams are working
around the clock to get their app built, tested, and released to hit their goals.

Fortunately, Exampli Corp recently integrated Prisma Cloud into their development lifecycle
adopting security from code to cloud. Once in production Exampli Corps operations
and security teams continue to leverage Prisma Cloud to monitor and protect runtime
resources, reduce the attack surface, and enforce least privilege.

Will The Exampli Corp team take the time to build a secure app? Or will the stress of rushing to complete the Bank of Anthos app in time lead to mistakes?

### Resources

Vulnerable IaC :

In this lab we leverage some intentionally vulnerable IaC. To learn more about the project and
its contributors visit the link below:

- https://github.com/bridgecrewio/terragoat

Bank of Anthos Application :

In this lab there is a mock banking application that is used as the application the Exampli Corp
development team is building. To learn more about the project and its contributors visit the link
below :

- https://github.com/GoogleCloudPlatform/bank-of-anthos

### Exercise

#### Cloud Security Posture Management

Cloud-native applications allow organizations to build and run scalable applications with great agility and resilience. However, they also present unique security challenges. Ensuring applications and services are secure at runtime is a core responsibility for security teams. CSPM tools can reduce the burden on cloud security teams by automating routine security monitoring, audits and remediations, allowing security teams to focus on high-priority items and prevent configuration drift. 

In this section, you will explore some use cases for securing GKE resources and services.

1. Login to [Prisma Cloud](https://app3.prismacloud.io/login).

2. Use the credentials provided by your Instructor to authenticate.

3. Let's start with taking a look at the **Asset Inventory** page to get an idea of the scale of resources that are being monitored by this particular Prisma Cloud tenant.

4. Begin by clicking on the **Inventory** tab at the top and click on **Assets**.

![Alt text for image](/screenshots/shift_left/cloud-security-posture-management-2.png "Optional title")

5. The **Asset Inventory** can be a helpful place to get a high level view on cloud assets and their compliance with defined policies. Without constant visibility of what is being deployed in your cloud footprint, you cannot begin to secure it.

6. Your screen should look similar to the one below:

![Alt text for image](/screenshots/shift_left/cloud-security-posture-management-4.png "Optional title")

7. We know the Exampli Corp team is using Kubernetes. Let's investigate further by clicking on **GCP** under the **Cloud** column. Here we can see all GCP services in use.

![Alt text for image](/screenshots/shift_left/cloud-security-posture-management-5.png "Optional title")

8. We can see several issues associated with **Google Compute Engine**. Click on this service name to drill down further. On the next page we can see issues associated with **Google Compute Engine VM Instance**. Click on the Total assets to investigate.

![Alt text for image](/screenshots/shift_left/cloud-security-posture-management-6.png "Optional title")

9. Click on the **gke-bank-of-anthos-default-pool-681c740d-ob6o** Asset Name. A side panel will open on the right side to quickly see an Overview, Attack Paths, Alerts, Vulnerabilities and more for this GKE cluster.

![Alt text for image](/screenshots/shift_left/cloud-security-posture-management-7.png "Optional title")

10. Let's take a look at the raw config for this resource by clicking on the **View Config** button

![Alt text for image](/screenshots/shift_left/cloud-security-posture-management-8.png "Optional title")

11. Here we can see the raw configuration for this GKE cluster.

![Alt text for image](/screenshots/shift_left/cloud-security-posture-management-9.png "Optional title")

12. To learn more let's investigate the findings associated with this GKE cluster. Close out the resource config and click on the **Attack Paths** tab.

![Alt text for image](/screenshots/shift_left/cloud-security-posture-management-10.png "Optional title")

13. Note the **Findings Types** and see how they correlate with the Attack Path graph. Click on the **Internet Exposure** icon within the graph. Here we can see all the services associated with the host that make it vulnerable to outside attacks.

![Alt text for image](/screenshots/shift_left/cloud-security-posture-management-11.png "Optional title")

14. Pan over to the right of the Attack Path graph and click on the **Privilege Escalation** icon within the graph. Here we can see that elevated privileges are assigned to the host. An adversary can destroy sensitive information stored in the cloud resources, making irreversible damage to Exampli's organization.

![Alt text for image](/screenshots/shift_left/cloud-security-posture-management-12.png "Optional title")

15. Let's revisit the Internet Exposure finding by reviewing the associated alert and finding out the proper remediation. Click on the **Alerts** tab.

![Alt text for image](/screenshots/shift_left/cloud-security-posture-management-13.png "Optional title")

16. Next, click on the Alerts ID for the **GCP VM instance that is internet reachable with unrestricted access (0.0.0.0/0)** policy. Here we can see an Overview as well as a Recommendation to resolve the issue.

![Alt text for image](/screenshots/shift_left/cloud-security-posture-management-14.png "Optional title")

17. Click on the **Recommendation** tab. Here we can see the necessary steps to fix the exposed asset. 

![Alt text for image](/screenshots/shift_left/cloud-security-posture-management-15.png "Optional title")

In addition to the asset inventory and leading cloud management capabilities, Prisma Cloud makes compliance incredibly easy. Let's move on to the next exercise on compliance.

#### Compliance in the Cloud

Many organizations struggle maintaining a grasp on compliance in the cloud. So far we have inspected Exampli's IaC and found some troubling trends. Additionally, at runtime many assets are still vulnerable due to risky configurations and careless development practices.

With multiple upcoming compliance audits bearing down on Exampli's CISO's calendar it's time to begin reporting on what is in a failed state and what needs to be done to get the organization's cloud footprint compliant.

1. Start by clicking the **Compliance** tab at the top of the UI. This page provides a high level view of all the unique assets and their associated adherence to various compliance frameworks and policies. When Prisma Cloud detects a violation of a policy it generates an alert.

![Alt text for image](/screenshots/shift_left/compliance-in-the-cloud-1.png "Optional title")

2. Leverage the filters to adjust the results and select **GCP** for the **Cloud Type**. Refine the filters even more and select the compliance framework **CIS v1.1.0 (GCP)**.

![Alt text for image](/screenshots/shift_left/compliance-in-the-cloud-2.png "Optional title")

3. Click on the Compliance Standard Name from the results to see which services have policies applied for that standard. Prisma Cloud provides a nice breakdown of each service type for easy referencing. 

![Alt text for image](/screenshots/shift_left/compliance-in-the-cloud-3.png "Optional title")

4. This provides a focused view of Exampli's GCP footprint and its adherence to this CIS Standard.

It looks like the **Networking** service has a policy failure. Click on the red "i" icon under the **Failed** column. This will give us a view of the assets associated with the CIS policy failure. Your screen should look similar to the screen capture below :

![Alt text for image](/screenshots/shift_left/compliance-in-the-cloud-4.png "Optional title")

5. Click on the **Alert ID** associated with the **default** Asset name. A side window opens that provides an Overview, Recommendation, Asset Config and Alert Rules. Additionally, the alert can be sent to a third party integration, like JIRA, for automated ticket creation. Reports can also be generated so you'll be ready for the next assessment and audit. 

![Alt text for image](/screenshots/shift_left/compliance-in-the-cloud-5a.png "Optional title")

![Alt text for image](/screenshots/shift_left/compliance-in-the-cloud-5b.png "Optional title")

In this lab we covered various topics around IaC security and CSPM but there are many additional features and capabilities within Prisma Cloud. Feel free to explore the UI and investigate different asset types.

## Summary \ Resources

The Prisma Cloud team here at Palo Alto sincerely hopes you enjoyed this workshop. Today, organizations need a growing set of capabilities to secure modern cloud applications. Implementing DevSecOps into your development and security workflows with Prisma Cloud can provide the increased speed and agility your organization needs to implement zero trust throughout the entire development lifecycle. Check out the resources below for more information!

[Live Workshops](https://bridgecrew.io/resource/workshops/)

[DevSecTalks Podcast](https://www.paloaltonetworks.com/devsectalks/)

[Supply Chain Security](https://bridgecrew.io/software-supply-chain-security/)

[Cloud DevSecOps](https://bridgecrew.io/cloud-devsecops/)

[Learn More](https://www.paloaltonetworks.com/prisma/cloud)

##### Sample Git Repositories

[TerraGoat - Vulnerable by design Terraform Infrastructure](https://github.com/bridgecrewio/terragoat)

[Cfngoat - Vulnerable by design Cloudformation Template](https://github.com/bridgecrewio/cfngoat)

[CdkGoat - Vulnerable by design AWS CDK Infrastructure](https://github.com/bridgecrewio/cdkgoat)

[BicepGoat - Vulnerable by design Bicep and ARM Infrastructure](https://github.com/bridgecrewio/bicepgoat)

[KubernetesGoat-Vulnerable by design KubernetesCluster](https://github.com/bridgecrewio/kubernetes-goattest)

[KustomizeGoat - Vulnerable by design Kustomize deployment](https://github.com/bridgecrewio/kustomizegoat)

[SupplyGoat- Vulnerable by design SCA](https://github.com/bridgecrewio/supplygoat)



