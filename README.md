# crmint
# Introduction:
The purpose of this repository is to versionize the first CRMINT pipelines created for the voucher burn audience creation use case.

# Context:
PVCP is transitioning from traditional ‘manual’ marketing to Precision marketing. Therefor, as a first challenge, the voucher burn use case was chosen to stabilize the implementation of CRMINT inside PVCP's data ecosystem.

# CRMINT setup:
 to install crmint, follow the quick start guide, using the dev repo instead of the master: 
 https://google.github.io/crmint/docs/quickstart/
 
### Tips:
- In the crmint setup, pull from the dev version not the master version, due to package conflicts the installation will fail otherwise.
- In the crmint setup always create your bigquery, storage and crmint instance in the same region (EU/ US...), or else exports and table creation will fail.
- Always specify 'success'/'failure' in starting condition of each job created, or else it will probably fail in this beta crmint version.
- Use global (project level) variables to specify your bigquery project id only once.

# CRMINT pipelines:
## SEA & DV360 Channel:
![SEA SV Pipeline](pipelines2.png)
Audience selection is rule based:
- We select only the french market as scope
- We filter out all burned or expired vouchers
- We only select sessions dating 30days for CP & PV (kept low for testing purposes, to be modified in production env) 
- We filter out all vouchers holders who have done a booking during the last 6 months
- We select only customers who have been at the last two funnel stages for PV & CP
- We select only mono-arrival customers for social (trialists)

## Emailing Channel:
![Emailing Pipeline](pipelines3.png)
Audience selection is rule based:
- We select only the french market as scope
- We filter out all burned or expired vouchers
- We only select sessions dating 30days for CP & PV (kept low for testing purposes, to be modified in production env) 
- We filter out all vouchers holders who have done a booking during the last 6 months
- We select only customers who have been at the last two funnel stages for PV & CP
- We select only multi-arrival customers for emailing (repeaters)

## Social Channel:
![Social Pipeline](pipelines1.png)
Audience selection is rule based:
- We select only the french market as scope
- We filter out all burned or expired vouchers
- We only select sessions dating 30days for CP & PV (kept low for testing purposes, to be modified in production env) 
- We filter out all vouchers holders who have done a booking during the last 6 months
- We select only customers who have been at the last two funnel stages for PV & CP
- We select only mono-arrival customers for social (trialists)

## Technical Monitoring:
The native technical mornitoring was chosen for this first use case: 
1. We will receive email notifications each time the pipeline is run to specify failure/success of execution.
2. Logs are avaialable for manual verification on the crmint webapp, for debugging and testing.

## Migration:
- To facilitate migration, project id variables and data set id variables have been set in crmint settings. To migrate the project to another location, simply change the variable values in the settings and test the pipelines.

# Campaign Monitoring:
TBD


