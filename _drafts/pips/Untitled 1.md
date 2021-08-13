# get_summary - getAverageResponseTimeSummary - getAvgResponseTimeStatForToday - getAvgResponseTimeStats

every time a user message is followed by an agent message, we are updating the rolling avg resp time with the ticket using the formula
```
rollingAvg = ((ticketData.avgResponseTime * replyCount) + currentAgentResponseTime) / (replyCount + 1);
```

and storing in the cache

while retrieving, we multiply the avgRespTime and the replyCount to get the total resp time

based on the day and timezone we split the resp time, and the num of replies

# average_agent_response_time - averageAgentResponseTime - getAgentAverageResponseTime - getAvgResponseTimeStats