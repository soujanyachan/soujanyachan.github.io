# bragaDOCio

| Key Deliverables                                                                                                                                                                                                                              | Expected Level of Achievement          | Actual Achievements                                                                                                            |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| Tresemme bot: Hair solutions bot with delayed message, external webview and Facebook integration.                                                                                                                                             | Deployment on Tresemme website         | Bot has been given for testing.                                                                                                |
| Utterance management dashboard: Tests whether training utterances go to the correct journey and stores the required data in a TSV. Utterances to be tested can also be added through the dashboard UI.                                        | Deployment on platform                 | Has been deployed on platform and actively used                                                                                |
| At bot: Agents can trigger journeys in the user widget by entering ‘@bot utteranceToTriggerJourney’                                                                                                                                           | Deployment on platform                 | Has recently been deployed. Will be improved using journey suggestions and further refinement.                                 |
| Health check for bots: A cron job run every ten minutes to run a user configured health-check test case to ensure bots are always up.                                                                                                         | Deployment to test the health of bots. | Was deployed. Has been shelved for the time being to iron out some other issues in the entire test-service.                    |
| Woocommerce integration using a WordPress plugin: A plugin that inserts the given bot into WordPress pages that use the Woocommerce plugin and also sends cart/checkout information back to YM’s controller for use by the bot (as an event). | Deployment for SuperBottoms website.   | Integration is done and the plugin is built. Bot is in the process of being deployed on website.                               |
| Added string to pdf generation in bots: Given a properly formatted string, we are able to return a dynamically generated pdf to the user.                                                                                                     | Deployment for all bots.               | Currently being used in bots as an when required. Further improvement in the form of converting html to pdf will also be done. |
| Mask sensitive message: For use by the studio team to mask sensitive user information from agents and also in the database.                                                                                                                   | Deployment for all bots.               | Currently being used in bots when necessary.                                                                                   |

-------

I have written scripts to quickly automate the process of obtaining data dumps with the required formatting for the client data requests. The script saves all data related to profiles and decrypts messages and outputs both JSON and CSV formats, so the client-facing team can easily cherry-pick the information that is required.

I have also written documentation for getting our internal staging setup running on multiple machines. I have also supported the new members of the Platform team in doing the same.

I provide support during training issues for bots.


# Self Appraisal - Soujanya Chandrashekar

## General

-   Interpersonal skills / Teamwork
    
    -   Provided support and guidance to new engineers especially in the form of setting up the dev environment and running the different microservices.
        
    -   Answered my peers' questions and often guided then on using/improving Service Desk features or on general codebase issues.
        
    -   Wrote a comprehensive JsDoc documentation of the executor and also documented multiple agent service features on Confluence.
        
    -   Worked with bot devs / product team to improve new / existing features iteratively
        
    -   Supported bot devs by reviewing code for bugs, especially SEA bots (agent service specific features), Titan/ Tanishq (video calling / agent features), SIA (SIP integration specific)
        
    -   Contributed to scaling engineering hiring
        
-   Quality of work
    
    -   Deployed services to staging for testing
        
    -   Fixed bugs involving a number of services and often investigated production issues
        
    -   Can defend technical decisions in code review feedback.
        
    -   Scoped and helped implement solutions for their project (voice / video calling / janus).
        
    -   Managed medium-sized projects with some instruction ( voice / video calling ).
        
-   Communication
    
    -   Provided clear and concise information/regular status updates about the tasks worked on during meetings.
        
    -   Promptly responded to communications I receive from customers and peers.
        
    -   Assessed other's code during code reviews
        
    -   Descriptive PR messages /commit messages
        
    -   Wrote effective and usable documentation for multiple features, keep them reasonably maintained
        
-   Problem solving
    
    -   Generally try unblocking myself first before seeking help
        
    -   Can break down problems/implementations into iterative steps
        
    -   Builds or iterates existing features for the benefit of all engineers (data parsing tools, platform related)
        
-   Growth, Self-education and learning
    
    -   Taken and passed the Microsoft Azure - AZ-203 course on my own time.
        
-   Accountability
    
    -   I use my time effectively and am able to prioritize my work.
        
    -   I follow through on my commitments to others and actively keep them aware of any challenges I face.
        
    -   I work well autonomously.
        

## Technical

-   **Agent Actions** - implemented an agent automated assistant module by reusing chatbot user-flow mechanisms and displaying responses in the agent UI.
    
-   **Email/dynamic text canned responses** - Improved the existing canned responses feature by allowing the use of Mustache expressions / variable data in the responses. Also added the canned dynamic response feature to the email editor and implemented a HTML type response for rich text editing in the case of email.
    
-   **Image preview** before upload - Improved the existing upload feature by displaying a preview of the uploaded image before upload, limited to one image draft per ticket and agent with the required pop up message error handling and information.
    
-   **Agent Auto-suggestions** - integrated an ML-based agent autosuggestion API into the Support tab UI.
    
-   **Janus**
    
    -   voice / video calling - Janus plugin integration in widget and event handling in agents-service backend (rest of the team handled major app changes)
        
    -   deployed the dockerized Janus WebRTC gateway on Kubernetes
        
    -   deployed coturn and redis on standalone VM for media streaming.
        
    -   Click to call using triggerJourney and autostartCall functionality as in Titan / Tanishq bot.
        
    -   Call transfer between agents (both SIP and webRTC)
        
    -   SIP integration with telephony infrastructure (discontinued)
        
    -   recording pipeline (in progress)
        
-   **Health Check** - An automated script run every ten minutes (cron job) to run a user configured health-check test case to ensure that all production bots are always up. Used XMPP over WebSockets and a dummy user to send messages to the bot to check liveness and send emails to the configured users.
    
-   Implemented bot functions by extending the backend APIs and adding them to executor, namely:
    
    -   app.transferTicket
        
    -   app.updateCollaborators
        
    -   app.htmlChatTranscript - return chat transcript in HTML format
        
    -   app.getAgents - returns agent availability data
        
-   smaller fixes and features:
    
    -   UI-related
        
        -   Chat transcript CSV / PDF download
            
        -   Location, video display in ChatLogContainer
            
        -   Whatsapp notification messages display in ChatLogContainer
            
    -   Backend related
        
        -   Added ticket reassignment log to help in diagnosing issues on the bot dev / user end.
            
        -   Fixed role-related bugs in securing API calls.
            
        -   Added jspdf to executor to help in string to PDF conversion.
            
    -   Both backend and UI changes
        
        -   Active tickets table display in the Overview tab.
            
        -   Showing current queue position of the ticket in widget.
            
        -   Source based inactivity timeout.
            
-   **Dyte Integration**: worked on integrating third-party communication platform as a service into our backend. Provided support to the mobile apps team regarding this. Was the POC with the external company and managed our internal requests.
    

## Improvements

-   I have a tendency to stick with what’s working and am not always open to new approaches.
    
-   I like to figure things out myself and sometimes I put off asking for help, which slows me down and fuzzes time estimations for task completion.
    
-   I am generally more comfortable completing tasks on my own, meaning that I miss out on collaborative coding and pair wise / group wise development.
    

## Plan:

-   **Technical**: fully integrated recording pipeline (and further projects as they come up).
    
-   **Learning goals**: docker and kubernetes for the recording pipeline, Typescript for a better agents-service backend and a better understanding of react hooks in order to work on the new app. Also would like to take the CKA/CKAD to validate my Kubernetes skills.
    
-   **Improvements**:
    
    -   Keep a set amount of time (eg: half day, depending on the size of the issue) before asking for support from team.
        
    -   Participate in group wise tasks.

____________

took a session on WebRTC implementation in YM on 7th Jan 2021
was part of the onboarding for inbox, took session on 
General Setup - 10th May
Tags, canned responses, ticket timeouts, agent actions - 11th May
Contacts, Visitors, WebRTC calling - 19th May

supported yusuf through the issues he faced with respect to UI and backend, esp on staging cluster and during testing of his features.

base contact feature is built and deployed, maintaining with the small fixes / additions required by the clients / devs.

translation feature, took RnD session on that as well on 2 july
