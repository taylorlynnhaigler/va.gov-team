# Flipper Notes
#### Objectives:  
**1. Allow for a controllable percentage be guided into the new application from a Drupal page (un/auth page)**  
Flipper should be able to do this no problem  
**2. Allow for a known list of email addresses to be allowed through into the new application from a Drupal page (un/auth page)**  
We can whitelist email addresses  
## Background
### When releasing to production in chunks, do we use Flipper UI or implimentation switches?

Progressive rollout is totally optional. Some teams use progressive rollout on some features but it is not a hard and fast rule.
If we want to do it progressively we can use Flipper UI -

https://department-of-veterans-affairs.github.io/veteran-facing-services-tools/platform/tools/feature-toggles/

As an example progressive rollout was used with direct deposit because they were unsure how many errors they
users would recieve as well as the types of errors they would recieve so they wanted to release the feature
to a small percentage of users to monitor errors closely.

Flipper UI is essentially some conditional logic that we use to wrap our components and can gate our components for
a percentage of users. It provides a value to the front end that we can use to conditionally show some other
component to those users so that they see somthing other than the feature when the page loads.

Flipper UI works based on data in our database, not EVSS

### When deploying the static page on Drupal, do we release the page progressively?

Static pages on Drupal are completely static, there is no progressive deployment on a page level with our Drupal implimentation. 


### Possible solution paths

Some of the common scenarios for building experiences on VA.gov lend themselves to a particular solution with
Flipper UI. Here are some of those scenarios - 

#### Unauthenticated page leading to a full page React app

When we need to give the user some information before they enter a full page React app we often do it with an unauthenticated page. This presents a difficulty with using Flipper UI for a progressive rollout since we can't block the user from getting to the unauthenticated page. A possible solution, and most likely the most simple solution, is to make the content on the unauthenticated page agnostic as to if the user will have access to the feature. This prepares them for the idea that when they hit the React app they may not see the information they are looking for. An example of this is the implimentation path taken by the direct deposit team where they did exactly this.

Another possible solution, albeit a more complicated one, is to isolate the area of the unauthenticated page that has content that specifically links to the React app and wrap this content inside a React [widget](https://department-of-veterans-affairs.github.io/veteran-facing-services-tools/getting-started/common-tasks/new-widget) and then wrap that widget inside some Flipper UI code. This will allow you to access the flipper value throgh redux and change this peice of content for users who are gated from the feature. 

![Flipper example](https://github.com/department-of-veterans-affairs/va.gov-team/blob/master/teams/vsa/teams/ebenefits/launch-playbook/images/Flipper_W3.png)

## Using Flipper on Drupal (Epic Draft)
### Story
VSA Teams need a way to deploy features on Drupal where there are static pages using a method that gives full and granular control over who sees resulting pages and when so that a gradual launch can get create the most amount of feedback with the least amount of exposure.

Flipper does a really great job of giving this control based on traffic percentage but only on components that are built using React, not static pages written in the Drupal CMS.

### Proposed Solution A
- Embed a React component in the static landing page that acts as an A/B switch between the legacy and new application.  This entrance would most likely look exactly like a login or action button that, upon clicking, is informed by Flipper which page to send the user to. We will also need to wrap the 686 form itself in a flipper component that redirects traffic that are not included in the test group to another page that is TBD

### Considerations
Eventually we may want to present the application directly and without authentication and to do this, we would operate Flipper with its intended behavior and wrap the application so a percentage of traffic moves through the new code vs redirected to the previous application.
- In GA, use a `no-follow` tag?
- Limit entrance pathways?
- Simply not allow direct/unauthenticated access until more UAT is complete?

### Tasks
- Create a high level thumbnail view of the different potential pathways and highlight where the React components would be located.
---
- There are a three potential routes to View Dependents and the 21-686c within VA.gov:
   - The current Add Dependents landing page: https://www.va.gov/disability/add-remove-dependent/
   - The Declare Dependents page (broken?) https://www.va.gov/disability/add-remove-dependent/add-dependent-form-21-686c/
   - The form search tool (if deployed ahead of 686 launch)
   - Google shows links to PDF versions of the form, and points to other 686 information and resources; no link to the eBenefits version of the 686 was found.
   - eBenefits requires users to be logged-in to view dependents or to access its implementation of the 686
- In implementing Flipper, the major pathways contemplated for users to get to View Dependents as well as the 686 itself: 
  1. Sign in and view
    - This will need a flipper component to split traffic between **View Dependents in VA.gov** and the **legacy eBenefits Dependents application**  
    - From the View Dependents page, another flipper component will split traffic to the **new online 686 form** and the **legacy eBenefits Dependents application**  
  2. Add or change your dependents
    - This will be hidden until at 100%
  - Given that traffic might inadvertanly see the url directly (from Google for exmaple)
- Document the procedure and order of events for unwinding any necessary Flipper components after allowing 100% of traffic through.
  - Leave in place to act as a future "valve"? 
  - What is the precedent?
- React Components to be built  `TODO:`
  - Landing page has an embed of....
  - Flipper configuration considerations `TODO:`
- Review and testing
  - RBPS
  - Stakeholders
  - GA
  - Errors in Sentry
  - Contact Center
  
### Potential Acceptance Criteria
- [ ] As an authenticated (LOA3) user, I can see a login button on the static landing page that uses the usual design pattern
  - [ ] Some predetermined percentage of the time, I will be presented with the new application, else, be sent to existing application as if nothing happened.
- [ ] The process is well documented and repeatable by other teams.
