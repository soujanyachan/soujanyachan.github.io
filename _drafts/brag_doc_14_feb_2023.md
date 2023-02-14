---
type: Journal
---

1. translation: offload the computation to a worker
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


#DRAFT

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
Implemented debug logs -
Implemented a basic canned responses search from the ui side
Implemented workflow builder in golang from scratch.

support/leadership 
Provided support for the detailed search
Provided multiple tutorials and wrote extensive documentation to help with liquibase migrations
Mentored for de integration
Supported services+inbox xmpp reliability implementation
Mentored for template format change and sending notification on report creation
video calling revamp? - settings in ui
better metrics tracking
Fixing chat names in transcript and in bot messages using profile and cdp names.
cdp integration with the help of cdp team
sip calling poc




okrs
- Elevate platform stability and security
  - *Resolution of critical and high issues reported by Snyk for inbox microservices
  - *All (relevant) features should be onprem ready
  - *All (relevant) features should be multi-region ready
- e2e engineering plannign
  - No. of late days for feature deployment
  - no of bugs in post prod
  - time bw planned and actual of feat dev
  - no of dev ready features in backlog
  - test coverage
  - regular dev planning/implementation details
- preditable and robust product delivery
  - end to end sprint planning on jira
  - reduction in spillover of stories / issues sprint on sprint
  - every feature should have one dev doc and one customer facing doc
