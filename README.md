# Portland Police Bureau Response Times

Analysis of how Portland Police Bureau (PPB) response times have changed against officer staffing and call workload, 2015 to 2026.

## Analysis
This repository does not contain the substantive analysis and reasoning. Below is a short summary of the findings as supported by the data.

### Background
Average response times by Portland Police Bureau since sometime in 2020 have increased notably. This has generated much discussion within the city of Portland. Portland Police Bureau maintains that reduced overall staffing levels prevent them from improved response times and they have asked for additional funding to address the concern. Their core contention is that more officers would improve response times.

### Hypothesis
The analysis sought to answer two questions at the heart of PPB's stance: is there a relationship between officers and response times? If so, would more officers reduce response times?

Stated affirmatively, more officers should reduce response times.

### Data & Methods
Using a public records request, a list of all PPB staff along with their active periods was supplied. Additionally, call data from the PPB's publicly available dashboard was downloaded. All data is accurate to July 2026. To get a month by month aggregation of the data and simplify the analysis, a date scaffolding table was used to interpolate the active periods for PPB staff.

### Officer Workloads and Response Time
Instead of raw call data, officer workloads were calculated based on the number of calls per officer. This allowed for fluctuations in staffing and call volume. Calls may go down, but so could active officers. The ratio of calls that an officer may have to handle is a better metric of PPB capacity than either calls or officers on their own.

Response time was averaged and did not use median. There are methodological shortcomings to a simple mean over a median. Early analysis checked for a meaningful difference in results but none was found. Obviously "meaningful" is doing a lot of work in that last sentence and curious minds are encouraged to take another look.

When workloads are mapped against response time, a scatterplot emerges with three (probably two) distinct clusters. These clusters map almost precisely to the period before June 2020 and the period after June 2020. A simple web search reveals that George Floyd Protests began around May of 2020. I have labeled these phases "Pre-Floyd", "Floyd/Pandemic", and "Recovery Periods" spanning 2015-May 2020, June 2020-December 2021, and 2022+ respectively.

### Pre-Floyd
This period has relatively low response times regardless of officer workload. In fact, as the workload increases response times vary only slightly. This suggests that in the Pre-Floyd pandemic, staffing had a minor but insubstantial relationship to response times. Put another way, even when case loads increased, other more important aspects not measured in the data affected response times.

This period serves as a useful baseline. It tells us what is possible under similar staffing, call volumes, and workload constraints. It also tells us that the hypothesis is probably not supportable.

But let's power on.

### Floyd & Pandemic
Initially I looked at March and April 2020 as my cutoff for the period, but all the way until May 2020 the data looks very similar to the Pre-Floyd period. It's not until June 2020 that response times drastically increase while workload remains the same. PPB has stated that they significantly re-allocated staff resources to handle ongoing protests, so it would track that workloads for officers are not fully reflected in the data here.

However, the trend of increasing response times continues into the Recovery period and today yet the workload remains within the same band as the Pre-Floyd period. To address a national misconception about Portland, Oregon directly, it's not a hell-hole. In fact, it's quite nice and calls to police are on the decline. So unmeasured riots really aren't affecting workload.

## Conclusion
PPB's response time woes are not the product of an officer staffing shortage.

### No Relationship
The startling conclusion is that PPB's staffing does not have a relationship to response times. While a minor but notable relationship existed, there is no way to explain response times through officer workloads since June of 2020.

### Caveats
1. Workloads and staffing _could_ still be responsible for the difference if something about staff levels, response times, and workloads is not captured in the data. However, and this must be emphasized strongly, PPB has not offered any specific change in the ways that they conduct their work as a reason nor have they supplied additional data to support their conclusion. The hypothesis as stated is the supplied reason in public testimony and statements by the office.

2. I'm just one person and subject to my own biases. I encourage additional analysis, discussion, and data that challenges my assumptions. I expect I missed something, that's how we learn and build knowledge.

## A Super Simple Description of the Analysis.
The number of calls is going down (good).
Response times continue to go up (bad).
The number of officers is fairly constant, but slowly increasing.
Workload (calls per officer) is also fairly constant.

If we accept that the number of officers affects response times, then this should not happen (response takes longer for fewer calls).

This pattern (response time increases, workload does not) begins after the George Floyd protests started. The protests stopped, but the (lack of) pattern has not.

## Charts

| | |
|---|---|
| ![Indexed monthly trends](IndexedMonthlyTrends.png) | ![Workload vs response time](WorkloadvResponseTime.png) |

## Repository layout

| Path | Contents |
|---|---|
| `Portland Police.designer.ipynb` | Notebook (Databricks Designer export) that loads the raw data, joins it by month, and builds the summary table |
| `Final Data/PPB-Simple.csv` | Monthly summary: total staff, officers, call counts, and average queue, travel, and response times (seconds) overall and by priority (high, medium, low) |
| `Raw Data/CallsforService/` | PPB dispatched-calls open data, one Excel file per year, 2012 to 2026 |
| `Raw Data/Staffing/` | Redacted PPB personnel records (police actions and EEO report), 2015 to 2026 |
| `Raw Data/FillDates-Month.csv` | Month list used to fill gaps in the monthly series |
| `Research/` | Reports on PPB staffing and recruitment used as background |

## Reproducing

The notebook was built in Databricks and its source paths point at a Databricks volume. To rerun it elsewhere, change the file paths in the `source_*` cells to the files under `Raw Data/`.

## Acknowledgements & Sources
Lots of people helped.

## AI disclosure

Claude (Anthropic's AI assistant) was used to help set up this repository: creating the GitHub repo, drafting the initial README, and adding the license files. It was not used for any analysis including the analysis in this README.

All data collection, analysis, and conclusions were done by hand with non-AI methods. Nothing in the data or the charts was generated or altered by AI. The notebook was built by hand through the Databricks Designer interface, a human-operated tool. Designer auto-generates the short descriptions and code headers on each cell (for example "Read CSV file with specified options"), but the choice and order of steps, and the logic of each, are the author's. The raw data, the processing steps, and the outputs are all included in this repository so that every result can be audited and replicated independently.

## Licensing

- **Code** (the notebook): [MIT](LICENSE).
- **Original analysis, charts, and `Final Data/PPB-Simple.csv`**: [CC BY 4.0](LICENSE-CC-BY-4.0.txt). Reuse freely with credit to Nick Hara.
- **Third-party material is not covered by either license.** `Raw Data/` and `Research/` come from PPB, the City of Portland, and the authors of the reports, and remain under their original terms.
