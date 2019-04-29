---
title: Notes and Thoughts from developing an AI/ML project in the Indian Government
layout: post
category: posts
published: true
---


**Context**: I work as a data scientist at Ministry of Rural Development, Government of India. Specifically in a department that is in-charge of boosting rural road connectivity across villages in India. Last year, I was put in charge of exploring an algorithmic method of selecting candidate roads for upgradation/repair keeping in mind connectivity to schools, hospitals and agricultural markets. 

It was a resource-constraint problem, we don’t have the budget to repair all the roads in our massive network, so the government had to ensure roads with maximum utility were prioritised. The definition of utility (a policy decision) was based on roads which most people depends on to access hospitals, markets and educational facilities. 

I proposed an algorithm which drew the shortest path from each habitation in a block (an administrative geographic division) to its nearest school, hospital and market in the block. Post that, it iterated through each road segment to identify the total habitations which depended on it and summed up the populations.

The idea was that if this road was to deteriorate, access to facilities for most number of people will be affected - making a case for preemptive repair/upgradation.

From code and pilot on QGIS to a paragraph in the final policy guidelines - it took multiple stakeholder presentations and negotiations spanning over 6 months. 

## Here are some of my thoughts/notes from the process:

### Fairness, Transparency and Accountability are not new concepts in Governance
Mechanisms of fairness, transparency and accountability are installed in government functioning over years and I found them to naturally flow (with some prodding) into the realm of automatic decision making or IT which to be them is another means to an end. Admittedly, the manifestation of FAT principles or questioning wasn’t exactly technical in nature. But I believe the nature of questioning can be expanded further given the first principles seem to exist. Some questions that I was posed came from a deep sense of equity and civic duties while some came from fear of internal government audits and  jaded experience with past failed IT projects.

### Can you calculate this on paper?
One of the questions which I was posed the most with was if I could replicate the outcome of the algorithm by hand on paper. I could identify two sources of concern which led to this questioning:
Assumption that the IT tool which would incorporate the algorithm wouldn’t work as proposed or would not be ready on time. If we were mandating the States to use this algorithm, as a fail-safe the algorithm should be easily replicable on paper by officials incase the system fails. 
The incumbent method of selection is rubric based point system and hence there is an ease of working with solutions which they understand how they function under the hood.

The proposed algorithm which was based on shortest path analysis isn’t easily replicable on paper.  I would assume that only simplistic approaches would meet this criteria and by-default these would be far more transparent or replicable. But I am unsure if the requirement to be solvable on paper necessary and thereby having something simplistic in itself is fair baseline - as such solutions might miss the nuances and complexities of realities present.

### Understanding the appeal of algorithmic decision making
I presented the algorithm to representatives of different States through workshops and visits. In general, they agreed with the intuition behind it. During the feedback sessions, what came unequivocally was there hope that this would limit political interferences by local representatives in the process of selection of roads. In their experience, there have been moments in which political local representatives have tried to pressurize them into selecting sub-optimal roads.

They believe that If they had a printed map which was system generated - they could point to that when they were pressured to select something else which may or may not be the most optimal choice. 

Ideally, in the spirit of democracy, the process of selection of roads allows for the political representatives to have a say as they are supposed to represent the needs of their constituents. But anecdotal experience suggests, interference is often malafide and driven by vested interests. 

The motivation to by-pass or subvert downstream corruptible interfaces of bureaucracy often leads to techno-solutionism and centralizing of powers further upstream in the decision making chain. 


### What if we are audited for our choice of roads?
Internal and CAG audits came up again and again while discussing with the officers at the central department in charge of monitoring and administering the scheme. The concern stemmed from creating process/policy which we won’t be able to enforce subjecting the department to endless back and forth with internal and CAG auditors. Though the primary subject of this concern was whether we choose to use the word may or shall in the framing of the policy, a part of the concern was also regarding the explainability of the algorithm in-case of audits and objects raised by auditors and political representatives (hypothetically antaganozied because their agency was challenged by an algorithm)


### Careful selection of point of intervention
If the final objective of the exercise is to ensure the output is utilized in decision making, the right point of intervention in an already existing policy needs to be identified. Often, the algorithm will have to function in an existing operational policy landscape and it won’t be possible to drop ship it.

This may involve the following:
 - Understanding exactly how the current process of selection happens in writing and reality (often not as they appear in high-incentive, easily corruptible environment).
 - Decoupling of existing processes to make space for intervention.
Eg. The shapefiles required for the algorithm were being uploaded digitally only after the selection of roads was completed and hence didn’t give a point of intervention.

Careful scoping of AI/ML interventions while understanding the constraints under which technology operates in Government is the key to successfully implementing these projects. 

### Importance of clear internal Accountability
The fact that I was internal and single-handedly pushing for this algorithm made it internally very easy to made accountable for incase things go awry. This acted as an additional personal incentive to be sure of what I advocating for. Although, I don’t think this is largely the case in other government technology projects especially if the solution was being proposed by a larger monolith corporation. The natural proposal is to ensure clear accountability measures for high priority projects. This would be two fold - better contract management with external vendors and having competent & clear roles designated inside the department for IT liaison. 

### Negotiations and transformations
By the end of the process a transformed version of the policy was adopted with the negotiations only leading to something more transparent, adjusted to the reality of IT in government and cautious of limitations of algorithms which were ignorant to local edge-cases and realities. I believe, this was only possible because of the amount of deliberation this “policy” decision was subjected to.

## What worked in favour of successful uptake of the algorithm

 - I proposed the algorithm  as a planning exercise called Trace Mapping. It makes it appear as a human conducting an exercise and preparing a map as against an omniscient off the shelf tool which gives an answer. It humanised the algorithm and made it easier to refer to in policy discussions.
 - It was a recommendation tool for planning as against a tool which mandated selection of roads from the list of options it generated. 
 - We found a way to approximately reproduce the algorithm on paper without any maths (simply tracing lines with a pencil). It made it less of a blackbox and also acted as the failsafe incase the IT tool failed. Even though shortest path analysis is not trivial mathematically, the output is extremely easy to interpret, verify and understand. It’s an open question whether I would have had the same reaction from the department had it been a machine learning model (even a linear regression for that matter)



## Open Questions and thoughts on using AI in the government:


### Fairness, Accountability and Transparency are not new conversations in governance and FATML shouldn’t operate with that assumption. 
Rather, what is that we can do to ensure traditional FAT principles in civil services seamlessly also translate into the realm of automated decision making at scale.

While accountability seems to stem from internal regulatory and audit based concerns, I have noticed fairness subjected to contextual and personal interpretation and ideals. While transparency is also more or less subjected to regulation (RTI) but not with the same associated weight as internal audits which can have serious consequences politically and individually to the careers of bureaucrats.

It’ll be interesting to understand interpretations of fairness by different levels of bureaucracy by conducting thought experiments contextualized in the realm of governance:

Eg. Once the policy mandated eligibility criterion for a scheme have been fulfilled - Is it fair to prioritise eligible beneficiaries based on their likelihood of succeeding in the intervention or it’s only fair to choose them at random?


### In my experience certain “automated decision making” systems I’ve chanced to work on previously didn’t face the same set of scrutiny as this project. 

Is it the nature of the algorithm or high-stakes nature of the situation? This algorithm was grey-box and hence approachable enough for officers to poke holes in it? Are problems of selection conceptually thought of differently then that of prioritisation or surveillance (exception management)?


More than supervised learning - not all “automated decision making” in the government will be in the form of supervised machine learning models. Some will be unsupervised learning problems or more commonly from the realm of optimization. As in the case above, recent discriminatory audit techniques on prediction might not directly apply.


### There is a need to translate well documented or otherwise issues which government technology projects face and translate how these will seep into ML/AI projects.

**Lopsided technical literacy between government and technical solution** providers leads imbalanced client-vendor dynamic. Though overtime and with practice, the technical literacy of bureaucrats has increased, it still leads to vendors getting the last (and not necessarily factually correct) say on most technical discussions. Often, under-resourced government departments don’t have dedicated ICT PMUs and are at the mercy of the vendor. 

This dynamic will be further carried forward with AI/ML projects. Further, even the vendors are not that technically literate at the moment. 

Eg I was asked to look at a pilot AI/ML project which officers and the vendor proudly boasting to have 85% accuracy (a term which the bureaucracy understood loosely, not technically). After probing the team and looking at their scripts, it appeared that the baseline itself was 85% and the model did no better than a classifier which predicted each case as the majority class.


**Technology project as a mean and not an end** Often times, IT projects which are not central to service delivery, are launched and forgotten. Eg. A hypothetical citizen feedback tool once launched isn’t monitored on the closure of complaints, the service level agreements, crashes etc. This may stem from the lack product ownership talent inside the government and contracts with vendors which end at the final release. But the case remains, the maintenance and monitoring of usage non-primary IT projects remains to be a weak point. Translating the same to the realm of machine learning projects would mean that models once trained and evaluated offline will potentially not be monitored post deployment for drifts in evaluation metrics, concepts and inherent distributions. 

Maintenance of machine learning models is not trivial and usually not taught in MOOCs which happen[*] to be the primary source of information for domestic talent in India till the time curriculum in universities adapt.

**Procurement and Contract Management:** Though briefly touched upon the previous point, contract management is poor in government in general and is amplified further when dealing with technical projects. It’s yet to be seen how contracts and DLI (Disbursement Linked Indicators) will look for machine learning projects. Though, this project was in-house, I’ve worked on 2 other pilots projects with vendors. A nuanced and retrospective reading of the contracts and deliberation on how they can be further improved is warranted. The good folks at USDS have been advocating Agile in procurement of government technology products. Will something similar work for AI/ML projects?


**Readiness of National Informatics Centre**: NIC is government’s technology arm. What’s their understanding of AI/ML projects? As the government’s go to agency for technology projects, how prepared are they for AI/ML? What role will they play in AI/ML projects and how can they better prepared? 

By my personal observation, the role of NIC in development has reduced as they wish to focus more on product management and ownership while development resources are hired from consulting firms through its NICSI arm.


### Data is not just biased, it's corrupt:
 Biased data isn’t particular to developing countries per-say. The problems of under-representation, feedback loops etc are being discussed widely in media and literature lately. 

Another manifestation of biased data is corrupted data which will be a problem more common to developing economies with high amount of street-level corruption. Usually the labels to predict are ones of high importance in decision making. The higher the importance in decision making, the more chances of it being corruptible. Eg. Let’s say one has fire-hazard inspection data for buildings in a city. There has been a budget cut and I’ve been tasked to prioritize buildings to inspect. As per one definition of efficiency, I want to get a 100% hit-rate in my inspections. So, I train a model on results of past inspections. There are two classes - hazardous & safe. A building labelled as safe can actually be safe or be hazardous but the inspecting officer was bribed to label it as safe. The chances of a building labelled as hazardous has a high chance of being hazardous given a building owner would litigate if wrongly labelled as hazardous even after following norms. The repercussions of training models on corrupted data needs to be understood further and data science methods to mitigate the effects of such models need to be explored as most of the high-stake data in government might be corrupted in this manner. 



### Variance in quality of data collection as a reflection of larger inequalities.

This isn’t just true to machine learning projects. A lot of time when evidence based policy think tanks are scoping for projects - they prefers geographies with quality administrative data systems/MIS etc. Functioning data systems are often manifestations of relatively functioning operations, bureaucracy and availability of resources. So, geographics which arguably need more focus are not selected for pilots/evaluations etc.

The same will be applicable to optimization and AI projects as well. For example, in our case of Trace Mapping, for the algorithm to function properly, the shapefiles submitted need to be clean ie the network should be complete, continuous and well split. Each state independently prepared their shapefiles and there is a clear variance in the quality which may be attributable to either their contract management, local remote sensing capacities etc. These States will be further punished (assuming using the algorithm has net positive gains) because the algorithm won’t function for them.

Similarly, this may also occur while working on supervised learning projects in which geographies with poor data will end up being chunked out in the data cleaning or scoping phase itself. 

*Blog posts are not intended to be final products, but rather a reflection of current thinking and/or catalysts for discussion, like tweets but longer. These thoughts are my own and don't represent that of the Government of India.*


======END======

Appendix:
[*] Based on my anecdotal experience while conducting more than 30+ interviews for machine learning engineer positions at Aspiringminds in 2016.

