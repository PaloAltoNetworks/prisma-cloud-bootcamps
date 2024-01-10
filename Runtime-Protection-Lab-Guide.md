# PRISMA CLOUD RUNTIME PROTECTION BOOTCAMP


### Lab Introduction

Thank you for joining today’s Runtime Protection camp. The lab will focus on application security within the software development lifecycle. Before we begin the lab let's start with a brief overview of the lab scenario to help frame the context.

### Scenario

The Exampli Corp, a mock corporation, is rushing to finish a new mobile banking app for their customers by the end of their fiscal quarter. Up against unrealistic goals the development and infrastructure teams are working around the clock to get their app built, tested, and released to hit their deadlines.

Fortunately, Exampli Corp recently integrated Prisma Cloud into their development lifecycle adopting security from code to cloud. Once in production Exampli Corps operations and security teams continue to leverage Prisma Cloud to monitor and protect runtime resources, reduce the attack surface, and enforce least privilege.

Will the Exampli Corp team take the time to build a secure app? Or will the stress of completing the Bank of Anthos app in time for deadlines lead to mistakes?

### Architecture 

The lab primarily focuses on Exampli Corp’s banking application known as the Bank of Anthos. The Bank of Anthos application is an example application purpose built for Google Kubernetes Engine, you can find the repo in the Resources section.

Prisma Cloud is integrated with mock company Exampli Corp in the following ways : 

1. Cloud Accounts are onboarded with Prisma Cloud allowing visibility into Exampli’s resources as well as their associated behavior and configuration states.

2. Critical applications in Exampli Corp’s cloud footprint are protected by Prisma Cloud defenders.

3. Code Repositories, Image Registries, and CI Tools are on-boarded into Prisma Cloud allowing for detection and remediation of misconfigurations and vulnerabilities earlier on in the development process.

### Resources

Vulnerable Repo:

In this lab we leverage some intentionally vulnerable code repository. To learn more about the project and its contributors visit the link below:

- https://github.com/bridgecrewio/supplygoat

Bank of Anthos Application:

In this lab there is a mock banking application that is used as the application the Exampli Corp is building. To learn more about the project and its contributors visit the link below:

- https://github.com/GoogleCloudPlatform/bank-of-anthos



### Protect Critical Applications

#### Visualize Applications and Establish Context 

The first step to protecting applications is to gain and maintain comprehensive visibility of your applications and all their associated resources. If Exampli Corp does not have oversight of their cloud environment it is impossible for them to stop emerging threats, respond to incidents, or reduce vulnerabilities. In a modern multi-cloud and hybrid world, applications are broken into different environments across the clouds like VMs, containers, serverless compute architecture types. Maintaining visibility is essential to protecting applications at runtime.

Prisma Cloud supports a massive amount of compute types, to review the supported systems check out our public documentation. (https://docs.paloaltonetworks.com/prisma/prisma-cloud/prisma-cloud-admin-compute/install/system_requirements)

Let's help Exampli Corp get a clear picture of the application running on their vulnerable GKE cluster. Start by taking a look at the microservices running the Bank of Anthos application using Prisma Cloud’s Radar feature.

1. Login to [Prisma Cloud](https://app3.prismacloud.io/login).

2. Use the credentials provided by your Instructor to authenticate.

3. The Radars feature lets you gain a bird’s eye view to monitor and understand your cloud applications. It helps you visualize the connectivity between microservices and search for vulnerabilities. Use the dropdown window in the upper left corner to select the **Runtime Security** focus and select **Containers** under the **Radars** section. Select the cluster **bank-of-anthos**.

![Alt text for image](/screenshots/runtime_protection/maintaining-visibility-1.png "Optional title")

4. Once you have selected the correct cluster your screen should look similar to the screenshot below:

![Alt text for image](/screenshots/runtime_protection/maintaining-visibility-2.png "Optional title")

5. Radar provides a visual depiction of the connections between containers, apps, and cluster services across your environment. Take some time to play around with the Radar feature and think through the following questions:

**What type of information can you learn by clicking on the nodes?
How does this visibility help you protect your applications?**

6. Let’s dive deeper into the **frontend:v0.5.5** microservice. Click on the associated container. Your screen should look similar to the screenshot below:

![Alt text for image](/screenshots/runtime_protection/preventing-attacks-3-v2.png "Optional title")

7. Take some time to review the **Vulnerabilities** page.

![Alt text for image](/screenshots/runtime_protection/preventing-attacks-4.png "Optional title")

8. Of the identified OS vulnerabilities, which one has the highest CVE? Do all the identified vulnerabilities contain a fix?

9. Take a look at the **Layers** tab to view the dockerfile that built this image and find where vulnerabilities were introduced.

![Alt text for image](/screenshots/runtime_protection/preventing-attacks-6.png "Optional title")

10. Find the file that added the most severe vulnerabilities and open it up by clicking on it to learn more about specifically what CVEs were added. Your screen should look similar to the screen capture below :

![openssl-1](https://github.com/c-haisten/c2c_summit/assets/98335592/7d522d07-18c8-4ce0-afe2-4d12cb44d370)

**We can see that this particular file introduced a ton of vulnerabilities including the usage of openssl version 1.1 which is susceptable to a number of malicious exploits.** 

11. Now that we have established some understanding of this container and have found some CVE's lets expand our knowledge by observing this workload's behavior using Prisma Cloud's forensic modeling capabilities. Click the back arrow at the top right hand side of the UI and arrive back at the container summary view. Your screen should look similar to the screen capture below :

![Alt text for image](/screenshots/runtime_protection/preventing-attacks-3-v2.png "Optional title")

#### Modeleing Application Behavior

Prisma Cloud observes and logs behavior such as running processes, network behavior, and even binary executions. Prisma Cloud then takes this data and builds a model for each workload giving administrators an understanding of what is the normal working conditions of their applications. Armed with this information administrators both understand the behavior of their workloads and can prevent malicious actions from taking place.

1. Begin by clicking on the forensic microscope underneath the **Runtime** tab.

![forensic-model](https://github.com/c-haisten/c2c_summit/assets/98335592/39476dcb-54cc-418e-bca4-cfeeb42cac71)

2. Here you can see all the events displayed. Let’s take a deeper look at these events to get some details and see what has been happening with our bank-of-anthos-frontend.

![Alt text for image](/screenshots/runtime_protection/investigate-incidents-at-runtime-5.png "Optional title")

3. To learn more please find the following documentation covering more details around runtime protection.(https://docs.paloaltonetworks.com/prisma/prisma-cloud/prisma-cloud-admin-compute/runtime_defense/runtime_defense_containers)

4. Now let's take a look at a summary view of some of the suspicious behaviors taking place on this workload. Please click the close button at the bottom left of the UI. You should be back at the summary page and your screen should look similar to the screen capture below :

![Alt text for image](/screenshots/runtime_protection/preventing-attacks-3-v2.png "Optional title")

5. Next, click on **Runtime** tab on the summary view. Here we can view highlights from the container's behavior and see if there are any security concerns with what the container is doing.

![runtime-events](https://github.com/c-haisten/c2c_summit/assets/98335592/92d8f7c6-a14f-4a7a-8420-07afcedd0125)

6. On this screen you will find a summarized list of findings from the defender including behavior that is not in the container's model. Your screen should look similar to the screen capture below :

![runtime-summary](https://github.com/c-haisten/c2c_summit/assets/98335592/d751a357-11a1-437a-a0c3-95e30404752d)

7. Discover any audit findings with tcpdump activity and click on it. If you have trouble finding it you can type tcpdump in the search bar at the top of the UI.

![runtime-summary-1](https://github.com/c-haisten/c2c_summit/assets/98335592/24adb5ff-5f69-43af-b388-8ab63ae9929b)

![runtime-summary-filter](https://github.com/c-haisten/c2c_summit/assets/98335592/d955e32c-eee3-45c2-8e80-3c9dd9d65d77)

8. This view provides an expanded understanding of the finding. We can see that Prisma Cloud alerted on this finding due to the default rule to alert on suspicious behavior. Administrators can configure their own rules alert on or block malicious activity.

9. Creating rules to defend applications is easy in Prisma Cloud by using the navigation bar on the left hand side of the UI and selecting **Runtime** under the **Defend** section.

![Alt text for image](/screenshots/runtime_protection/preventing-attacks-9.png "Optional title")

10. On this page administrators can configure rules that make sense for their applications. There is a great deal of granularity given to Prisma Cloud administrators to configure allowed process, networking, and file system activities. Prisma Cloud defenders are also integrated with Palo Alto Network's WildFire anti-malware service allowing for the blocking of malware found on the application.

![runtime-rules-blocking](https://github.com/c-haisten/c2c_summit/assets/98335592/3b0f5dcb-7e1f-4668-bf90-40d41964bf41)

**Because this is a lab you will have limited permissions and are not able to edit or create rules, however feel free to explore the different pages.**

For more information about runtime rules and protection from Prisma Cloud check out our public documentation here. (https://docs.paloaltonetworks.com/prisma/prisma-cloud/prisma-cloud-admin-compute/runtime_defense/runtime_defense_containers)

#### Web Application Firewall and API Security

In addition to image scanning, runtime visibility and protection; the Prisma Cloud defender also provides Web Application Firewall and API Security.

1. To take a look let’s navigate back to **Radars -> Containers** and ensure you are viewing the **bank-of-anthos** app.

![Alt text for image](/screenshots/runtime_protection/maintaining-visibility-2.png "Optional title")

2. The green firewall log indicates that the front-end microservice is protected by Prisma Cloud.

3. Administrators can define rules to provide web application and api security capabilities to protect web applications. Prisma Cloud supports VM Hosts, Containers, Embedded Applications, and function deployment architectures.

![Alt text for image](/screenshots/runtime_protection/preventing-attacks-10.png "Optional title")

4. Administrators can define Custom Rules that provide Virtual Patching capabilities to protect against attacks exploiting CVE’s that have not yet been patched. For example check out the log4j blog where you can find more information about custom rules that were created to protect our customers. [Link](https://www.paloaltonetworks.com/blog/prisma-cloud/log-4-shell-vulnerability/)

5. Take a look at some of the attacks the defender has detected by navigating to **Monitor -> Events -> WAAS for containers**.

![Alt text for image](/screenshots/runtime_protection/preventing-attacks-12-v2.png "Optional title")

6. Let’s dive into one of the **OS Command Injection** attacks. Click the **total** value to view the events.

![Alt text for image](/screenshots/runtime_protection/preventing-attacks-13-v2.png "Optional title")

7. Select one of the entries and answer the questions below:

What was the result of the attack?
Was it blocked?
What was the http method that was used in the attack?
What container image was attacked?


## Summary \ Resources

The Prisma Cloud team here at Palo Alto sincerely hopes you enjoyed this workshop. Today, organizations need a growing set of capabilities to secure modern cloud applications. Implementing AppSec into your development and security workflows with Prisma Cloud can provide the increased speed and agility your organization needs to implement zero trust throughout the entire development lifecycle. Check out the resources below for more information!

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

