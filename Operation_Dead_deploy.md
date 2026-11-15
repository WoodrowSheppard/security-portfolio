# ["Investigating a policy compliance break in Azure"]

## Scenario
An Intern was given contributer access for a test enviroment. The test envierment created violated naming policies put in placen and was left over the weekend.

## Environment
Live multi-user Azure training tenant, Reader access.

## Investigation
1:
I located the test environment, and confirmed that it had violated the naming policies.
<img width="1923" height="1031" alt="image" src="https://github.com/user-attachments/assets/e71deb10-30d2-401b-8aa3-587a9d046cdc" />
2.
explored and investigated the deployment.
<img width="1918" height="1082" alt="image" src="https://github.com/user-attachments/assets/4de5a48c-1600-4f50-b808-e7182f8fc7d8" />
3.
Gleaned what I could from the deployments tags. In this case, who made the environment.
<img width="1917" height="1087" alt="image" src="https://github.com/user-attachments/assets/312a099d-43e7-4e29-9862-7f902ef888a2" />
4.
Checked the security settings at in the scope of the subscription.  
<img width="1256" height="641" alt="image" src="https://github.com/user-attachments/assets/469f1251-8e6b-4183-9f9c-74de8b62c9d3" />
5.
After not finding anything at the subscription level, I tightened my scope to the policies of the environment. I found a non compliant policy relevant to the naming problem.
<img width="1918" height="1091" alt="image" src="https://github.com/user-attachments/assets/7fd611e2-6c16-4029-95c4-f943b218c8c6" />
6.
Upon studying the policy, it would seem that the effect type is set to audit and not deny. Thus allowing the environment to exist against policy compliance.
<img width="1912" height="1087" alt="image" src="https://github.com/user-attachments/assets/9e71f9d0-92f6-4303-a69a-02582511ad25" />

## What broke / what surprised me
What initially surprised me was the layer of the environment that the non compliant policy was found in. I would have that that this vulnerability would appear somewhere in the security tab on the subscription layer. in retrospect, it makes since that the alert would appear in the policy section of the environment itself if it triggered an audit compliancy break. 

## Findings and recommendations
I found that the problem is that the policy that is in charge of upholding the strict naming conventions of this subscription was set to audit. I would recommend setting the effect type of this policy to deny, since there should be no reason to allow a resource in this subscription to defy the naming policy.

## What I learned
I learned:
- How to gather information about policy breaks from multiple parts of the Azure blade.
- The need to make sure every policy is set to the correct effect type.
- When to check the security of a subscription vs when to check for policy compliance breaks.

