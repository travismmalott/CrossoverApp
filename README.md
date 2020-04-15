1.	# Root Cause Analysis of the AES EDI (Jira Issue No.: AESEDI-53447)
2.	 
3.	## Date
4.	2020-04-15
5.	 
6.	## Authors
7.	*Travis Malott* -
8.	*CloudOpsEngineer*
9.	 
10.	## Status
11.	Resolved
12.	 
13.	## Summary
14.	The customer did not received the data from AES EDI.
15.	The investigation showed that the file with the data was actually sent.
16.	It was not processed due to an issue with the AES CIS service [Jira Issue No: AESCIS-38263].
17.	 
18.	## Impact
19.	486,000 records were affected.
20.	EDI to CIS monitoring service were affected as per the CIS side.
21.	 
22.	## Root Causes
23.	Customer Information Service could not process the file due to lack of available resources.
24.	 
25.	## Trigger
26.	Customer reported no records have been processed.
27.	 
28.	## Resolution
29.	Restarting the *AES CIS* monitoring service allowed us to spot the missed records that were not discovered automatically
30.	and where they were stuck.
31.	Re-running Garbage Collector freed enough resources to properly process all 486,000 records.
32.	 
33.	## Detection
34.	Our customer create this Jira to alert us on this failure. *Please refer to (AESEDI-53447)*
35.	 
36.	 
37.	## Action Items
38.	| Action Item | Type | Owner | Bug |
39.	| ----------- | ---- | ----- | --- |
40.	| Write monitoring policy to detect records missings | prevent | JRT | **Done** |
41.	| Set monitoring on a third-party in order to have no Single-Point-of-Failure | prevent | JRT | **ToDo** |
42.	| Create auto-scaling group of our workers to avoid this incident in the future | prevent | JRT | **On Going** |
43.	| Monitor the data ingesters and processors (ETL) | prevent | JRT | (Jira Issue No: AESCIS-38263)**ToDo** |
44.	| Validate adjacent architecture to verify correct monitoring and scale-out policies | prevent | JRT | **ToDo** |
45.	 
46.	## Lessons Learned
47.	We need to validate that our monitoring architecture fits our SOA infrastructure.
48.	 
49.	## Timeline
50.	 
51.	2020-04-15 (*all times UTC*)
52.	 
53.	| Time  | Description |
54.	| ----- | ----------- |
55.	| 10:45 | Issue reported |
56.	| 11:56 | SRE logged on console to validate architecture health |
57.	| 11:56 | SRE logged on CIS platform to check monitoring agents |
58.	| 11:56 | SRE restarted monitoring service |
59.	| 11:56 | SRE validated files processing status |
60.	| 11:56 | SRE discovered records missing|
61.	| 12:05 | SRE re-sent records to process |
62.	| 12:15 | SRE validated correct data processing of the records files |
63.	| 13:00 | SRE validated correct completion of the data processing of all the 486,000 records files |
64.	| 13:15 | SRE modified monitoring agent to correct view Service health |
65.	| 13:25 | SRE elevated change to set AutoScaling on these resources |
