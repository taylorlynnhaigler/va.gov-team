## Documented Design Decisions & Frequently Asked Questions

### Why can veterans only self-schedule into clinics that they've been seen at within the last 24 months?
- Many facility + care type combinations have an overwhelming numbr of clinic options. Furthermore, many of these clinics are confusing to veterans, because they're not consistently named in a way that's useful to veterans or even written in plain english.
- Certain clinics have specific uses that aren't obvious to veterans (for example, for new patients only), so opening up all available clinics for self-scheduling for everyone results in many cancelled or rescheduled appointments.

### Legacy VAOS includes a messaging dashboard to facilitate back-and-forth chats between veterans and schedulers. Why does the redesigned VAOS not have this feature?
- In usability testing, veterans were confused by the different communication options they have for their VA healthcare, and tended to think that messaging is done through Secure Messaging.
- Most veterans used the 'message a scheduler' feature to communicate more details about the appointment request or medical condition, and didn't expect to have bidirectional convrsations through the interface.
- The redesigned VAOS tool allows veterans to submit one message to a scheduler within the flow of creating an appointment request, and they can also see that message repeated back to them later in their pending appointments list.

### Why does the veteran not select an appointment cancellation reason?
- There are only three possible cancellation reasons that a veteran can select in the legacy application. In usability testing, veterans were confused by the three options and what the information was being used for at the VA.
- Of the three options, the 'unable to keep appointment' cancellation reason is sufficiently broad to accurately encompass most specific reasons that a veteran may use to cancel an appointment.
- Upon doing discovery into these cancellation reasons, the redesign team found the data to not be used for anything or reported on at any level. Thus, the team opted to simplify the veteran experience by removing the question.
- The 'unable to keep appointment' reason, if available for a facility, is auto-filled when cancelling.

### Can you track who cancelled an appointment (VA vs. veteran)
- Not currently, though we have heard from veterans and schedulers that it is frustrating to have the VA cancel an appointment, and similarly from schedulers that it's important to know whether the VA or a veteran cancelled a given appointment.
- Legacy VAOS does not have this capability either.

### Why is the facility timezone used when displaying appointment times to veterans?
- Veterans may be booked to receive care in a timezone that isn't their own residential timezone. In these instances, it is more useful to tell the veteran what time their appointment is in relation to the location of the appointment, since they will need to physically be in the facility's timezone at the time of the appointment.

### Why are you not using the standard Forms chapter progress bar in the VAOS appointment form?
- Because the flow of the form is so forked depending on which options you select. It isn't really a linear booking process that maps cleanly to the concept of progressing through different chapters.

### What type of 'add to calendar' action is triggered when someone clicks that link from their confirmation page?
- .ics file (iCalendar) is downloaded with specific appoitnment information. iCalendar files should work for Microsoft Outlook, Google Calendar, and Apple Calendars, but some may require a conversion to .csv 
- In the future, we will be looking to create a 'calendar widget' to enable more calendar functionality 

### How far in the past will appointments be pulled to determine available self-schedule clinics?
- 24 months (confirm with Jeff, may be 12 months presently).

### How would a veteran be blocked from excessive no-shows?
- Just as with legacy VAOS, there is no mechanism to 'turn off' someone's ability to use VAOS based on count of no-shows.
- Through discussion with Shawn Adams, this situation is annoying when it arises but is actually quite rare.

### How are 'registered VA systems' derived?
- ?? Presumably some VA system has a list of system IDs and associated ICNs
- The data source and logic for this is not being updated and should work the same as legacy VAOS

### Why 'confirmed appointment' and 'pending appointment request'
- ?? Lauren / Ryan

### Why is there not an 'office hours' question in the request flow?
- Because veterans are already signifying their preferred appointment dates and general times (am / pm), this question is redundant.

### Can a veteran change their residntial address that's used in the CCE calculation?
- Not currently, though we are exploring post-MVP enhancements to the CCE experience

### Why are 'nutrition' and 'podiatry' not Community Care types of care?
- Because CCE API (which is the API that the redesigned VAOS ultimately uses to check CC eligibility) is not currently able to check CC eligibility for these two types of care. This functionality is roughly expected in December, and VAOS will be updated as soon as those types of care are functional in CCEP API.

### The legacy VAOS application has a modal when you start it that tells you to not use VAOS for urgent care - why does the redesigned application not have this?
- The redesighned application has several similar prompts that are more contextual.
  - On the static page preceding the application (va.gov/heatlh-care/schedule-view-va-appiontments), there is an alert banner on the page noting that veterans should contact a care provider through other means if they have an urgent issue.
  - A red Veterans Crisis Line button is present on every page on VA.gov
  - Depending on the date choices a veteran makes within the self-schedule flow, conditional alerts let them know that there may be faster means of getting care.
  
### The legacy VAOS application has a 'hamburger menu' that allows veterans to update their email / phone contact info, as well as opt in / out of notifications. Why doesn't the redesigned application have this menu?
- VA.gov includes a centralized account prefrences hub that spans all tools and intgrates with VA-adopted 'source of truth' databases / systems to ensure that all veteran information is consolidated and up-to-date.
- While diting contact prefrences for an individual request is not possible in the MVP, veterans still have the ability to provide an email and phone of their choosing while scheduling / requesting to schedule an appointment.
- Post-MVP discovery work is needed on improving notifications overall because veterans don't currently find them useful. As part of this work, the redesign team will consider options for how best to integrate notification preferences into VA.gov's account infrastructure.

### The legacy VAOS application has a link to a user manual. Why doesn't the redesigned application have a manual?
- The manual is baked into the application, in the sense that actions that users can take are explained in plain language within the flow of the application itself. The scheduling flow is set up as a step-by-step wizard specifically to reduce cognitive overhead for veterans and eliminate confusion about what to do.

### How can veterans submit feedback about the new tool?
- A ForeSee survey will show to veterans on the confirmation page, once they complete their appointment scheduling process.

### Why does the new application not have a 'call before booking' option like the legacy application does?
- Because all veterans should receive a phone call before their appointment is finalized in order to reduce miscommunication / missd appointments and improve veteran satisfaction.
- The front end will auto-submit this option for all appointment requests

### Why does the new application not have a 'send me updates' option?
- Because appointment-level notification preferences are not editable, we have opted to send updates to all veterans so that no communication from the VA is missed.
- The alternative would have been to not send anyone updates, which would be a bad experience.

### The email and phone number contact information is being prefilled for veterans; where is this information coming from?
- Data is taken from the veteran's account preferences on VA.gov, which generally tie into Vet360.
- Phone numbers are mobile when available, or home when no mobile provided.

### Does changing email / phone in the appointment booking flow update the veteran's profile?
- No, it does not update their VA.gov / vet360 contact info. This is stated to vetrans on the contact info page as well.

### Why is there no facility info in the appointments list and other similar places?
- Facility details come from a separate endpoint that is not integrated into VAOS presently. The team is working to integrate this data source in order to show a richer variety of data about facilities to veterans.

### What's the maximum number of requests & appointments that a veteran can make?
- Request maximum is based on a facility's settings
- No maximum for self-scheduled appointments, just like legacy VAOS

### Why is there no 'prepare for appointment' in the appointment list?
- The content information is duplicative of the information contained both within the flow of the app as well as the individual facility pages.
- The full-fledged 'prepare for appointment' that's on legacy Staging isn't in production in legacy VAOS, so it was deemed to be out of scope for the redesign MVP.
- The redesign team is aware of important 'appointment information' that schedulers pass along to veterans through this field and is exploring integrating it into the appointment views.

### Why is 'express care' not a type of care that is offered through the new VAOS?
- The redesign team did discovery work on express care and found that it was more of a care modality than a specfic / separate type of care.
- Veterans were consistently confused by 'express care' in usability testing.
- ?? Lauren / Ryan - integration of express care isn't off the table, but needs more discovery

### Why do healthcare systems on the system selection page not show a state like legacy VAOS?
- VA healthcare systems may be spread across multiple states, so showing a state isn't necessarily accurate.

### Are 'resolved / no schedule' appointment requests displayed?
- No, the filtering in the new application mirrors the legacy VAOS application, which similarly does not include resolved appointments.

### Why does the new VAOS tool not ask for a preferred location for a CC appointment?
- Veterans have the ability to enter preferred provider contact info if they have a specific provider they'd like to see.
- We are usign the veteran's residential vet360 address to assume that they want to be seen somewhere near where they live, which should line up with their CC eligibility data.

### Why is 'podiatry' not available in the VA request flow?
- Podiatry has not yet been turned on or configured by VHA across most sites. Thus, it isn't possible to offer scheduling a VA request for that type of care. This should change in the coming months.

### Why is 'primary care' not available in the Community Care flow?
- Primary Care should be coordinated through a veteran's VA primary care physician to ensure that a doctor with context of a patient's needs gets a chance to think about the issue. Thus, if a veteran has an active assignment to a PACT, a veteran should not be able to make a primary care appointment at a Community Care facility without his or her VA doctor coordinating that care. This coordination is outside the scope of VAOS, so VAOS will only allow scheduling Primary Care appointments in the community if a veteran does not have an assigned PACT.

### How are Submitted Requests displayed in new VAOS, seems different than legacy VAOS? 
- Yes, in VAOS-R we are displaying requests for the last 30 days based on submitted date whereas legacy VAOS displays up to 3 months of requests and shows all request statuses.
  - For requst with status 'submitted' show
  - For requests with status 'Cancelled' show them if there's a request date later than today 
  - For requests with a status of Cancelled, we show them if there's a requested date later than today
  - For any other request statuses, we do not show
- What we're not showing for requests:
  - Any request submitted more than 30 days ago
  - Cancelled requests where all of their requested dates are in the past
  - Requests with a status other than Cancelled or Submitted
  
### Previously Seen business logic:
- Veterans are only able to use online scheduling if they’ve been seen at the selected facility for that type of care in the past 2 years. VAOS will automatically check their completed appointment history to make this determination.
- This logic applies to all care types/specialities including Primarcy Care and Mental Health. 

### For Direct Schedule - in legacy VAOS, Veterans were always shown a list of available clinics, but for new VAOS that busines logic was altered. Why? And what is the new business logic?
- Why: A key design principle for new VAOS is ensuring that Veterans are only seeing options that are available to them. This principle also applies to new business in which Veterans are only enabled for self schedule for VA appointments if they have been previously seen for that type of care at that specific VAMC. 
- If the veteran was previously seen (i.e. had a previous appointment for the ‘type of care’ selected) within the last 24 months, they are shown a list of the clinic(s) from those appointment to expedite self-scheduling.
- If the veteran selects “I need a different clinic”, when they are not seeing a clinic they are familiar with or used in the past, they are always forwarded to the appointment request workflow. This logic specifically deviates from previous VAOS app logic where legacy VAOS showed all available clinics regardless if the Veteran had be seen by specific clinic in the past. This along with nonsensical clinic naming convention led many Veterans to schedule into the wrong clinic. 
- We realize we’re being conservative in new VAOS, where some available/open self-schedulable clinics are not showing up. It’s a tradeoff, and it’s an experiment. The idea is – if we send you down the request flow, a human can actually help you get routed to a new clinic (and ideally, the right one for your situation). Next time you schedule, that clinic will show up as an option for you.
- We will want to watch this as part of user feedback and schedule manager feedback as part of new VAOS availability. 

### Legacy VAOS used to ask Veterans the following question when making a Community Care request - "How far are you willing to drive?" Why does new VAOSR not ask this question?
- We removed the question for 3 reasons:
   1. Veterans expressed during research sessions that they always defaulted to the lowest number when asked that question. 
   2. Now with the new CCE API, drive-time eligibility is calculated in the background as part of Mission Act, so the question becomes irrelevant.
   3. Mission Act basis eligibility on minutes (for distance) vs. miles (for distance).
- CC eligibility takes into account both - the grandfather 40 mile distance eligibility (built into the E&E static codes and carried over from Veterans Choice Program) and drive-time via Mission Act. The grandfather criteria is distance based eligibility in miles. Drive-time eligibility via Mission Act is based on average drive times and calculated in minutes (not miles). That criteria is 30 minutes for PC/MH and 60 minutes for speciality care. Here's a reference to the Community Care Eligibility fact sheet. The CCE API uses both static E&E (which includes this grandfather distance criteria) and drive-time. 
- A Veteran can be eligible for CC via static codes (such as distance), but not drive-time. Since the static eligibility check is 40 miles or less, that's why we default to 40 miles and do not show the question.
- Here's a reference to the [Community Care Eligibility fact sheet](https://www.va.gov/COMMUNITYCARE/docs/pubfiles/factsheets/VA-FS_CC-Eligibility.pdf). 

