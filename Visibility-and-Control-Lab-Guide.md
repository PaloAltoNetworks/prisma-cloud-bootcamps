# PRISMA CLOUD VISIBILITY AND CONTROL BOOTCAMP


### Lab Introduction

Thank you for joining today’s Visibility and Control camp. The lab will focus on the ways
that Prisma Cloud can help you secure cloud assets through posture and compliance tools.

Before we begin the lab let's start with a brief overview of the scenario to help frame the
context.

### Scenario

The Exampli Corp, a mock corporation, is rushing to build a number of cloud based applications before their fiscal year ends.
Up against challenging deadlines, the development and infrastructure teams are working
around the clock to get their app built, tested, and released to hit their goals.

Fortunately, Exampli Corp recently integrated Prisma Cloud into their development lifecycle
adopting security from code to cloud. Once in production Exampli Corps operations
and security teams continue to leverage Prisma Cloud to monitor and protect runtime
resources, reduce the attack surface, and enforce least privilege.

Will The Exampli Corp team take the time to build a secure app? Or will the stress of rushing to complete their apps in time lead to mistakes?

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

The cloud allows organizations to build and run scalable applications with great agility and resilience. However, the cloud also presents unique security challenges. Ensuring applications and services are secure at runtime is a core responsibility for security teams. CSPM tools can reduce the burden on cloud security teams by automating routine security monitoring, audits and remediations, allowing security teams to focus on high-priority items and prevent configuration drift. 

In this section you will explore how Prisma Cloud can help security teams inventory the applications and services running in their multi-cloud footprint. 

1. Login to [Prisma Cloud](https://app3.prismacloud.io/login).

2. Use the credentials provided by your Instructor to authenticate.

3. Let's start with taking a look at the **Asset Inventory** page to get an idea of the scale of resources that are being monitored by this particular Prisma Cloud tenant.

4. Begin by clicking on the **Inventory** tab at the top and click on **Assets**.

![Alt text for image](/screenshots/shift_left/cloud-security-posture-management-2.png "Optional title")

5. The **Asset Inventory** is a helpful page in Prisma Cloud where teams can get a high level view of their cloud assets and their compliance with defined policies. Without constant visibility of what is being deployed in your cloud footprint, you cannot begin to secure it.

6. Your screen should look similar to the one below:

![Alt text for image](/screenshots/shift_left/cloud-security-posture-management-4.png "Optional title")

7. Begin by clicking on **AWS** under the **Cloud** column.

![](/screenshots/v-and-c/Screenshot2024-02-13at2.52.38PM.png)

8. Here you will see a list of all discovered AWS cloud services for Exampli Corp. Prisma Cloud inventories the services and displays associated misconfigurations and vulnerabilities.

Feel free to explore any of the services to learn more about them.

![](/screenshots/v-and-c/Screenshot2024-02-13at2.50.00PM.png)

9. Because Exampli Corp's upcoming application is running on EC2, let's explore the Amazon EC2 Service Name.

In the **Service Name** column, click on the **Amazon EC2** service.

![](/screenshots/v-and-c/Screenshot2024-02-13at3.01.23PM.png)

10. Now we can see all the associated asset types for Amazon EC2. This includes the EBS Volume and EC2 Elastic Address for example. 

Let's learn more about the EC2 Instances themselves. Click on the value under the **Total** column in the EC2 Instance row.

![](/screenshots/v-and-c/Screenshot2024-02-13at3.01.23PMcopy.png)

Your screen should look similar to the one below.

![](/screenshots/v-and-c/Screenshot2024-02-13at3.09.53PM.png)

Here you can see all of the EC2 Instances and associated details, including Alerts, Vulnerabilities and Account information.

11. Let's take a look at the **PANW-WebServer-awsjamconfig** Asset.

![](/screenshots/v-and-c/Screenshot2024-02-13at3.45.29PM.png)

A sidecar window will open with an overview along with other tabs for investigation.

![](/screenshots/v-and-c/Screenshot2024-02-13at3.46.54PM.png)


12. To learn more let's investigate the **Findings** tab.

![](/screenshots/v-and-c/Screenshot2024-02-13at3.57.11PM.png)

Here you can see this EC2 instance is exposed to the internet and is not configured with Instance Metadata Service v2 (IMDSv2).


13. Next click on the **Attack Paths** tab to see a graphical view of the findings.

![](/screenshots/v-and-c/Screenshot2024-02-13at4.04.53PM.png)

Explore the icons within the Attack Path graph. In the screenshots below we can see the assets that are exposed to the internet as well as the IMDSv2 misconfiguration. 

![](/screenshots/v-and-c/Screenshot2024-02-13at4.13.32PM.png)

![](/screenshots/v-and-c/Screenshot2024-02-13at4.14.17PM.png)

14. Prisma Cloud keeps an inventory of alerts making it easy for security teams to prioritize the most important findings. 
15. Close the sidecar window by clicking the X at the top right of the screen and click on the **Alerts** tab at the top of the UI. 

![](/screenshots/v-and-c/Screenshot2024-02-13at4.24.07PM.png)

16. The **Overview** tab is an inventory of alerts with filtering capabilities to isolate what is most important. Feel free to try out the different filters. Admins are able to save filters to create customized views.

17. Next, let's take a look at the **Highest Priority** tab. This tab lists the highest priority alerts within the last 24 hours. If no findings are populated use the Time Range filter to increase the length of time. Keep this in mind moving forward. 

![](/screenshots/v-and-c/Screenshot2024-02-13at4.31.37PM.png)

18. Now let's click on the **Incidents** tab. The Incidents tab filters events that depend on audit/network logging and monitoring of runtime events via an agent.

![](/screenshots/v-and-c/Screenshot2024-02-13at5.23.29PM.png)

Click on the **Traffic from a suspicious IP address associated with Cryptominer activity** policy to expand the alerts and then click on an Alert ID to open a sidecar window to get an Overview, Anomaly Details and Recommendation for remediation. 

![](/screenshots/v-and-c/Screenshot2024-02-13at5.30.04PM.png)

![](/screenshots/v-and-c/Screenshot2024-02-13at5.37.01PM.png)

19. Next let's explore some more **Risky Attack Paths**. On this tab you can find an inventory of attack paths present within Exampli Corp's network. 

![](/screenshots/v-and-c/Screenshot2024-02-13at5.52.45PM.png)

Scroll down and click on the **Data exposure risk due to AWS S3 hosting static website contains sensitive information** policy to expand the alerts and then click on an Alert ID to open a sidecar window to review the evidence. Feel free to explore other events.

![](/screenshots/v-and-c/Screenshot2024-02-13at6.00.52PM.png)

20. Close the sidecar window and click on the **Exposure** tab next. This view shows all Network policy type violations within Exampli Corp's assets.

![](/screenshots/v-and-c/Screenshot2024-02-13at6.08.15PM.png)

Let's investigate the **Azure Virtual Machine in running state that is internet reachable with unrestricted access (0.0.0.0/0)** policy. Click on the policy to expand the alerts. Click on one of the alerts to see an overview and recommendation to resolve the issue.

![](/screenshots/v-and-c/Screenshot2024-02-13at6.19.35PM.png)

![](/screenshots/v-and-c/Screenshot2024-02-13at6.20.28PM.png)

21. Close out any sidecar windows and select the **CIEM** tab to discover resources that have misconfigured permissions. 

![](/screenshots/v-and-c/Screenshot2024-02-13at6.24.23PM.png)

Click on the **AWS Lambda Function with IAM write permissions** policy to expand the alerts. Click on one of the alerts to see an overview and recommendation to resolve the issue.

![](/screenshots/v-and-c/Screenshot2024-02-13at6.35.57PM.png)

![](/screenshots/v-and-c/Screenshot2024-02-13at6.38.31PM.png)




In this section we explored the various filtered views of alerts discovered by Prisma Cloud. In the next section we will focus on Compliance. 

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



