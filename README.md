Data Folder README
This folder contains all datasets used in the capstone synopsis:
AI and ML Enabled Transaction Workflow Optimization for Group Operations in
Banking and Finance.
All data is derived from two publicly released event logs of the same
Dutch financial institute, separated by a documented system change:
> van Dongen, B.F. (2012). *BPI Challenge 2012* [Data set]. 4TU.ResearchData.
> https://doi.org/10.4121/uuid:3926db30-f712-4394-aebc-75976070e91f
> van Dongen, B.F. (2017). *BPI Challenge 2017* [Data set]. 4TU.ResearchData.
> https://doi.org/10.4121/uuid:5f3067df-f10b-45da-b98b-86ae4c7a310b
Between the two releases, the institute deployed a new case-management
system (the BPIC17 dataset documentation states explicitly that the new
system "allows for multiple offers per application"). This real,
documented system change is used as the intervention for the interrupted
time-series analysis in RQ3.
Combined Dataset Overview
	BPIC12 (pre)	BPIC17 (post)	Combined
Cases	13,087	31,509	44,596
Events	262,200	467,443	729,588 (after stage filter: 702,923)
Date range	2011-10-01 to 2012-03-14	2016-01-01 to 2017-02-01	~ 5.4 years
Coverage	~6 months	~13 months	19 sequential months
File Inventory
#	File	Rows	Nature	Used for
1	combined_panel.csv	74	Stage-month panel, pre (BPIC12) + post (BPIC17)	RQ1, RQ3, RQ4
2	combined_balanced_sample.csv	1,000	Case-level balanced 50/50 classification sample	RQ2
3	combined_stage_summary.csv	4	Stage-level descriptives	Descriptives
4	combined_prepost_summary.csv	8	Era-level (pre / post) summary by stage	RQ3
5	data_dictionary.csv	25	Variable-level dictionary	All files
Activity-to-Stage Mapping
Both event logs are mapped into the same four critical stages. BPIC12
activity names are in Dutch; BPIC17 names are in English.
Stage 1: Application Intake and Validation
BPIC17: A_Create Application, A_Concept, A_Submitted, A_Accepted, A_Complete, A_Validating, A_Incomplete, W_Validate application, W_Handle leads
BPIC12: A_SUBMITTED, A_PARTLYSUBMITTED, A_PREACCEPTED, A_ACCEPTED, W_Completeren aanvraag, W_Valideren aanvraag, W_Afhandelen leads
Stage 2: Offer Preparation and Dispatch
BPIC17: O_Create Offer, O_Created, O_Sent (mail and online), O_Sent (online only), W_Assess potential fraud
BPIC12: A_FINALIZED, O_SELECTED, O_CREATED, O_SENT, W_Beoordelen fraude
Stage 3: Customer Response and Callback
BPIC17: O_Returned, W_Call after offers, W_Call incomplete files
BPIC12: O_SENT_BACK, W_Nabellen offertes, W_Nabellen incomplete dossiers
Stage 4: Final Decision and Closure
BPIC17: A_Pending, A_Cancelled, A_Denied, O_Accepted, O_Refused, O_Cancelled
BPIC12: A_APPROVED, A_DECLINED, A_CANCELLED, A_REGISTERED, A_ACTIVATED, O_ACCEPTED, O_DECLINED, O_CANCELLED, W_Wijzigen contractgegevens
Month Index Convention (for ITS)
Months 1..6 correspond to BPIC12 (2011-10 through 2012-03); `intervention_deployed = 0`
Months 7..19 correspond to BPIC17 (2016-01 through 2017-01); `intervention_deployed = 1`
The change point t* = 7 marks the first post-system-change month observed
The compressed sequential index assumes the institutional process is the primary object of study; calendar gap between 2012 and 2016 is acknowledged as a natural-experiment feature in the synopsis Limitations section
Data Provenance
BPIC17: GitHub mirror `Patrick-Megard/ProcessMining-Loans`, file `Datasets/Loan_all_events.csv`, extracted from the .xes.gz at the 4TU.ResearchData DOI above.
BPIC12: GitHub mirror `ERamaM/PredictiveMonitoringDatasets`, file `raw_datasets/BPI_Challenge_2012.xes.gz`, parsed with pm4py.
Retrieval date: 2026-04-19.
Reproducibility
Running `python3 build_data_combined.py` (Python 3.10+, pandas, numpy,
pm4py) with the raw input files at the hard-coded paths reproduces every
file in this folder byte-for-byte under random seed 18.
Ethical and Privacy Notes
Both BPIC12 and BPIC17 have been anonymized and publicly released by
their owner for research use. No personally identifiable information is
present. Use follows the 4TU.ResearchData licence distributed with the
original logs.
