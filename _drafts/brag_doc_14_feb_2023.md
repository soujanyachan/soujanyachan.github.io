1. translation: offload the computation to a worker. 
2. /internal/message/bulkUpdateMessageWithTranslations
3. on prem tickets
4. health check - need to test anf deploy
5. wa template
6. dyte integration
7. message search using elasticsearch
8. supported for the detailed search
9. liquibase migration document - mentored multiple
10. proactive notifs
11. no code email ticketing v1
12. recheck liveness and readiness probes for agents service
13. auto translation for the video calling - subtitles, symbl
14. cache settings
15. de integration - video calling - supported
16. notifications - CHECK METRICS
17. xmpp reliability implementation
18. human_takeover
19. refactor of get ticket api in all controllers for da team
20. priyanka template
21. events
22. pprof
23. debug logs
24. canned responses search
25. contact prefix search ?
26. dyte webhook handle
27. added multiple scripts and apis for dev exp for debugging and on call.

OKRs
- Elevate platform stability and security
  - Resolution of critical and high issues reported by Snyk for inbox microservices - 50/100. This was being followed properly in the beginning of the quarter with a call to fix this every Tuesday however, since this is reported separately from the triage and is not usually checked during code reviews this has gotten off track.
  - All (relevant) features should be onprem ready - 50/100. As a company we are not moving forward with prioritizing onprem deployments, this is paused as a goal for now.
  - All (relevant) features should be multi-region ready - 100/100. All our features are multiregion ready. We have ensured that the relevant database liquibase migrations happens for each change, as well as any configuration changes. We deploy to every region by default and don't do custom development for any region. If by any chance some scripts need to be run in a specific region the codes/configs are still committed to the same master branch scripts file to ensure jobs can be run in the same way in all regions.
- e2e engineering planning improvements
  - No. of late days for feature deployment - 14 vs 7 -  On avg around 2 weeks. Depending on the scope of the development and how many teams are involved.
  - no of bugs in post prod - 100% - We do not find major bugs in post prod sanity due to rigorous testing by QA team in conjunction with the devs of that feature.
  - time between planned and actual of feature development - 14 vs 7 -  On avg around 2 weeks. Depending on the scope of the development and how many teams are involved.
  - no. of dev ready features in backlog - This is improving and on track due to our regular grooming and engineering planning calls.
  - test coverage - this is on track. All new deployments are strictly going out with tests.
  - regular dev planning/implementation meetings - 100% - we are having regular dev planning meetings
- predictable and robust product delivery
  - end to end sprint planning on JIRA - 100% - all issues are tracked on JIRA.
  - reduction in spillover of stories / issues sprint on sprint - 20% - We are having spillover, usually due to bandwidth issues but we are working on taking up fewer new tasks per sprint and pushing back on unverified development.
  - every feature should have one dev doc and one customer facing doc - 100% - Every new feature we are putting out has at least an engg planning document.

# DRAFT

Handled on-call in a rotation, in the beginning of the year focussed more on on-prem and multiregion rellated issues. Now more related to bugs and general knowledge gap issues.

Implementation
Implemented and maintained the video calling dyte integration, also adding new features such as the symbl-based translation and transcription and upgrades.
Implemented message search using elastic search - Message search pipeline - Exact Match Search
Implemented proactive notifications
Implemented no code email ticketing v1
Implemented notifications e2e
Implemented the changes for human_takeover for the active learning project, this way the transfer to agent is tagged in the messages
Refactored ticket API in all controllers for the da team for push to druid
Implemented events changes for both chat and ticketing
Implemented debug logs 
Implemented a basic canned responses search from the ui side
Implemented workflow builder in golang from scratch.
video calling revamp? - settings in ui
better metrics tracking
Fixing chat names in transcript and in bot messages using profile and cdp names.
cdp integration with the help of cdp team
sip calling poc

support/leadership 
Provided support for the detailed search
Provided multiple tutorials and wrote extensive documentation to help with liquibase migrations
Mentored for de integration
Supported services+inbox xmpp reliability implementation
Mentored for template format change and sending notification on report creation

Tech debt
test coverage
  - regular dev planning/implementation details 
  - end to end dev planning on jira
