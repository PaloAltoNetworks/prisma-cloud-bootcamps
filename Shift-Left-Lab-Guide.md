# PRISMA CLOUD SHIFT LEFT BOOTCAMP


### Lab Introduction

Thank you for joining today’s Shift Left camp. The lab will focus on the ways
that Prisma Cloud can help you secure Infrastructure as Code or IaC from the code to runtime.

Before we begin the lab let's start with a brief overview of the scenario to help frame the
context.

### Scenario

The Exampli Corp, a mock corporation, is rushing to finish a banking app for
their customer Bank of Anthos in time before the fiscal year ends.
Up against challenging deadlines, the development and infrastructure teams are working
around the clock to get their app built, tested, and released to hit their goals.

Fortunately, Exampli Corp recently integrated Prisma Cloud into their development lifecycle
adopting shift left security from code to cloud. Once in production Exampli Corps operations
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

Let's begin by exploring the power of shifting security left with Infrastructure as Code scanning. As infrastructure is being defined as code, security must be integrated with the tools developers use.

Fortunately, Prisma Cloud can be integrated into the development pipeline and tools developers use to secure IaC. Prisma Cloud IaC security is built on the open source project Checkov. Checkov is a policy-as-code tool with millions of downloads that checks for misconfigurations in IaC templates such as Terraform, CloudFormation, Kubernetes, Helm, ARM Templates and Serverless framework.

To learn more visit: https://www.paloaltonetworks.com/prisma/cloud/infrastructure-as-code-security

In this exercise, we will take a look at some IaC templates within Exampli Corp’s repository.

#### Find and Fix Insecure Infrastructure Code

1. Login to [Prisma Cloud](https://app3.prismacloud.io/login).

2. Use the credentials provided by your Instructor to authenticate.

3. Use the dropdown window in the upper left corner to select the three different security focuses within Prisma Cloud. Select **Application Security**.

![Alt text for image](/screenshots/shift_left/find-and-fix-insecure-infrastructure-code-3.png "Optional title")

4. Next, use the navigation pane on the left to select **Projects** under the **Code** section.

![Alt text for image](/screenshots/shift_left/find-and-fix-insecure-infrastructure-code-4.png "Optional title")

5. Click on the **IaC Misconfiguration** tab and in the **Repositories** drop down, select the **c-haisten/Exampli** repository

![Alt text for image](/screenshots/shift_left/find-and-fix-insecure-infrastructure-code-5.png "Optional title")

6. Once you have selected the correct repository, filter by "High" severity and let's take a look at some troubling misconfigurations found in the GCP Terraform templates. Click on the search icon ![Alt text for image](/screenshots/shift_left/search-icon.png "Optional title") and search for **SQL**

![Alt text for image](/screenshots/shift_left/find-and-fix-insecure-infrastructure-code-6a.png "Optional title")

![Alt text for image](/screenshots/shift_left/find-and-fix-insecure-infrastructure-code-6b.png "Optional title")

7. Now that we have filtered by severity and search term, explore the different misconfigurations and
click on the Resource associated with the **_GCP SQL database is publicly accessible_** policy.

![Alt text for image](/screenshots/shift_left/find-and-fix-insecure-infrastructure-code-7.png "Optional title")

8. Note the side panel window after clicking the policy. Click on the **See policy documentation** hyperlink to see guidelines on how to resolve the
misconfiguration. Below is an example of how the policy box will look and the type of information you will see.

![Alt text for image](/screenshots/shift_left/find-and-fix-insecure-infrastructure-code-8.png "Optional title")

9. Reviewing the guidelines we can see the description of this misconfiguration, its potential risk, and how to remediate at build time and runtime.

![Alt text for image](/screenshots/shift_left/find-and-fix-insecure-infrastructure-code-9.png "Optional title")

10. Now navigate back to the Prisma Cloud platform. Click on the associated SQL database resource and view the helpful information about the misconfiguration such as its history, errors, details, and traceability. It also will give you an option to view the resource in its VCS.

![Alt text for image](/screenshots/shift_left/find-and-fix-insecure-infrastructure-code-10.png "Optional title")

11. This misconfiguration makes the database available to the internet. This database contains Personally Identifiable Information such as user credentials and financial information. By using Prisma Cloud code security, the Exampli Corp security team can avoid costly mistakes and protect the integrity of the database and application. 

**There are many other examples to explore in the Exampli repo, feel free to use the filters and search bar to explore additional resources and findings.**

#### Generating Pull Requests

1. Depending on the nature of a misconfiguration, Prisma Cloud can provide single click remediation. This capability creates a pull request that is sent to the version control system where the IaC template is stored.

Looking at the same **big_data.tf** template, there is another HIGH severity misconfiguration for lack of SSL on SQL database connections.

![Alt text for image](/screenshots/shift_left/generating-pull-requests-1.png "Optional title")

2. This resource is a fully managed relational database service for MySQL, PostgreSQL and SQL Server. It is recommended to enable SSL but we can see it is not configured in this resource's template.

**The Suppress and Fix capability requires increased RBAC capabilities and is not available to read-only users**

3. Pull requests have been created previously for various findings. To access the VCS associated with this IaC resource click the git link under the Details tab. We can also see the developer who committed the last change associated with this IaC resource.

![Alt text for image](/screenshots/shift_left/generating-pull-requests-3a.png "Optional title")

![Alt text for image](/screenshots/shift_left/generating-pull-requests-3b.png "Optional title")

4. After clicking the git link we see the last commit associated with the **big_data.tf** IaC template. Highlighted is the **ip_configuration** parameter which does not include the SSL enablement.

![Alt text for image](/screenshots/shift_left/generating-pull-requests-4.png "Optional title")

5. To view the fix generated by Prisma Cloud let's take a look at the pull requests tab at the top of the github UI.

![Alt text for image](/screenshots/shift_left/generating-pull-requests-5.png "Optional title")

6. Once on the Pull Requests view take a look at the [PR](https://github.com/c-haisten/Exampli/pull/1) and its associated [commit](https://github.com/c-haisten/Exampli/pull/1/commits/a79745d0a19acc3418db6fcd7ce40e11659de75a). Examining the changes, the ‘require_ssl = true’ setting has been added to the big_data.tf template.

![Alt text for image](/screenshots/shift_left/generating-pull-requests-6.png "Optional title")

Now that you have discovered the power and ease of remediating code fixes with Code security, let's explore how to detect and remediate exposed secrets embedded within Infrastructure as Code. 

#### Identify Exposed Secrets

According to the [2023 Verizon Data Breach Report](https://www.verizon.com/business/resources/T34b/reports/2023-data-breach-investigations-report-dbir.pdf), **74%** of all breaches include the human element, with people being involved either via Error, Privilege Misuse, Use of stolen credentials or Social Engineering.

Fortunately, Prisma Cloud makes it easy for anyone to quickly determine how the exposed secret can harm your organization and what steps must be taken. 

1. From the Projects page, click on the **Secrets** tab and click on the **AWS Access Keys** secret type for the **providers.tf** file. Make sure the SQL search from the previous exercise is cleared. 

![Alt text for image](/screenshots/shift_left/identify-exposed-secrets-1.png "Optional title")

2. Take a closer look at the **providers.tf** template in the side panel window. Here we can see an access key hardcoded in the template. Click on the **Manual Fix** button to be taken directly to the file on github. From there you can see the full template and make necessary changes. 

![Alt text for image](/screenshots/shift_left/identify-exposed-secrets-2a.png "Optional title")

![Alt text for image](/screenshots/shift_left/identify-exposed-secrets-2b-v2.png "Optional title")

3. When accessing AWS programmatically, users can select to use an access key to verify their identity, and the identity of their applications. An access key consists of an access key ID and a secret access key. Anyone with an access key has the same level of access to AWS resources. These exposed AWS access credentials could let an unauthorized attacker access the Exampli Corp AWS account.

**We recommend you protect access keys and keep them private. Specifically, do not store hard coded keys and secrets in infrastructure such as code, or other version-controlled configuration settings.**

### Software Composition Analysis:

1. While in the **Projects** view, click on the **Vulnerabilities** tab and ensure that you select the **c-haisten/bank-of-anthos** repository in the Repositories filter.

![Alt text for image](/screenshots/runtime_protection/software-composition-analysis-5.png "Optional title")

2. Once you have selected the correct repository, it will show you all the security incidents found in the code of that branch. Let’s check to see if there are any serious vulnerabilities by filtering **Severities -> High.**

![Alt text for image](/screenshots/runtime_protection/software-composition-analysis-6.png "Optional title")

3. Next, we will select a CVE ID to investigate the vulnerability and determine what next steps to take. Prisma Cloud gives us several options for how to interact with the vulnerability.

Administrators can click suppress, or fix. The suppress button allows you to dismiss all incidents that fall under that specific policy violation. The fix button will allow you to remediate the vulnerability via a bump fix. Here we can see that the vulnerability can be fixed easily by bumping from v1.49.1 to at least v1.53.0.

**Suppress and Fix requires increased RBAC that is not available in this lab**

4. You can also click the “Details” or “Issues” tab on the right side of the page to get some more information on the dangers of the specific vulnerability.

![Alt text for image](/screenshots/runtime_protection/software-composition-analysis-8.png "Optional title")

5. This CVE has a CVSS score of 7. It makes Exampli Corp’s Bank of Anthos app vulnerable to information leaks and privilege escalation. 

On this page Exampli Corp developers can gain context on the CVE and click on the link to NIST providing them with all the details and documentation regarding the vulnerability.

Now that we have found some vulnerabilities and secrets violations in our Application code, let's take a look at how Prisma Cloud can give us visibility to the package manager files that comprise applications by taking a look at the Software Bill of Materials (SBOM).

### Software Bill of Materials

1. While in the **Application Security** view, use the navigation pane on the left side and click **SBOM** under the **Visibility** section and ensure that you select the **c-haisten/bank-of-anthos** repository in the Repositories filter.

![Alt text for image](/screenshots/runtime_protection/software-bill-of-materials-1.png "Optional title")

2. Next, use the search bar on the right side to search for **crypto**.

![Alt text for image](/screenshots/runtime_protection/software-bill-of-materials-2.png "Optional title")

3. Click on the **cryptography** package to see additional information such as version, license type and vulnerabilities. 

![Alt text for image](/screenshots/runtime_protection/software-bill-of-materials-3.png "Optional title")

4. Next, take a deeper look at the cryptography package file by looking at the **Issues** and **Repositories** tabs.

![Alt text for image](/screenshots/runtime_protection/software-bill-of-materials-4a.png "Optional title")

![Alt text for image](/screenshots/runtime_protection/software-bill-of-materials-4b.png "Optional title")

5. In the Issues tab, how many vulnerabilities are present in the cryptography package? Use the dropdown window to locate CVE's and read more about them. 

![Alt text for image](/screenshots/runtime_protection/software-bill-of-materials-5.png "Optional title")

6. Use the Repositories tab to discover which file is introducing the vulnerable software package. How many repos are impacted? Is it in the same location or multiple?

## CI/CD Risks and Visibility

CI/CD pipelines streamline application coding, testing and deployment through continuous integration and delivery. CI/CD has many benefits when it comes to operationalizing application workflows, but with this advancement in application developments comes risks. That's why it's important to have security In, Of and Around the pipeline. Let's look at a couple examples of how Prisma Cloud can protect pipelines. 

1. While in the **Application Security** view, use the navigation pane on the left side and click **Technologies** under the **Visibility** section. Click on the **Pipeline Tools** tab to see what technologies are present in the pipelines monitored by Prisma Cloud. 

![Alt text for image](/screenshots/shift_left/cicd-risks-visibility-1.png "Optional title")

2. Here we can see a nice overview of all technologies present with insights, descriptions and the associated vendor. Click on the **Python** Tool Name to open the side panel window. Here we can gather further information like details of the tool, which pipelines are leveraging the tool and how it's being used.

![Alt text for image](/screenshots/shift_left/cicd-risks-visibility-2.png "Optional title")

3. Exit out of the side panel window and click on **CI/CD Risks** under the **CI/CD** section. Here we have a nice visual breakdown of all risks associated with our pipelines.

![Alt text for image](/screenshots/shift_left/cicd-risks-visibility-3.png "Optional title")

4. Click on the **Excessive user permissions to a repository** Risk Name. A side panel window will open with an overview showing risk location in the delivery chain, details and steps to solve.

![Alt text for image](/screenshots/shift_left/cicd-risks-visibility-4.png "Optional title")

5. Click on the **Open Events** tab to see all open events associated with a particular risk. From here security teams can pinpoint exactly where the risk is being introduced and resolve the issue. 

![Alt text for image](/screenshots/shift_left/cicd-risks-visibility-5.png "Optional title")

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



