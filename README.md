# epa-model-airmod

API for AERMOD modelling system

The following, are some references we must consume in order to obtain knwledge.

**The user guide for AERMET: **

[User's Guide for the AERMOD Meteorological Preprocessor (AERMET)] (https://gaftp.epa.gov/Air/aqmg/SCRAM/models/met/aermet/aermet_userguide.pdf)

AERMET provides a general-purpose meteorological preprocessor for organizing
available meteorological data into a format suitable for use by the AERMOD air quality
dispersion model. This user's guide provides instructions for setting up and running the
AERMET preprocessor

**Creating Web APIs with Python and Flask:**

Learn how to set up a basic Application Programming Interface (API) to make your data more accessible to users. This lesson also discusses principles of API design and the benefits of APIs for digital projects.

[Creating Web APIs with Python and Flask](https://programminghistorian.org/en/lessons/creating-apis-with-python-and-flask)

**How to Create an API in Three Steps - Stoplight Blog:**

[How to Create an API in Three Steps - Stoplight Blog])https://blog.stoplight.io/how-to-create-an-api-in-three-steps)

So you’ve  and would like to create your own. While it can certainly feel like a daunting task, with a methodical design-first approach, you’re sure to come away with a useful API of your own. This post will cover the three basic steps when creating an API:

## Functional keyword/parameter reference

The keywords are organized by functional pathway and
within each pathway the order of the keywords is alphabetical, excluding the keyword that
identifies the start of a pathway. The pathways used by AERMET are as follows, including the
applicable AERMET processing stages and the in the order in which they appear in the tables
that follow:

**JOB** - for specifying overall JOB control options (all stages);

**UPPERAIR** - for processing NWS UPPER AIR data (Stages 1 and 2);

**SURFACE** - for processing NWS hourly SURFACE data (Stages 1 and 2);

**ONSITE** - for processing ONSITE meteorological data (Stages 1 and 2);

**MERGE** - to MERGE the three data types into one file, including 1-minute ASOS wind data, if available (Stage 2);

**METPREP** - for METeorological data PREParation for use in a dispersion Model (Stage 3).

Two types of data are provided for each pathway. The first data lists all of the
keywords for that pathway, identifies each keyword as to its type (either mandatory or optional,
either repeatable or non-repeatable, and if it is reprocessed), and provides a brief description of
the function of the keyword. The second type of data, which may take up more than one page,
describes each parameter in detail.

The most external data for the JSON file is,

```json
[
  JOB: {
    "Keyword": "JOB",
    "Type": ["Optional", "Non-repeatable"],
    "Description": "Start of JOB pathway. This statement is optional if the statements associated with this block appear first in the input control file",
    "CHK_SYNTAX": {
      "Keyword": "CHK_SYNTAX",
      "Type": ["Optional", "Non-repeatable"],
      "Description": "Flag indicating that only the syntax of the input statements should be checked for errors, i.e., no data are processed."
    },
  },
  UPPERAIR: {},
  SURFACE: {},
  ONSITE: {},
  MERGE: {},
  METPREP: {},
]
```

<!--
=====================================================================
-->
