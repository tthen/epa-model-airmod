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
{
  "JOB": {
    "Keyword": "JOB",
    "Type": ["Optional", "Non-repeatable"],
    "Description": "Start of JOB pathway. This statement is optional if the statements associated with this block appear first in the input control file",
    "CHK_SYNTAX": {
      "Keyword": "CHK_SYNTAX",
      "Type": ["Optional", "Non-repeatable"],
      "Description": "Flag indicating that only the syntax of the input statements should be checked for errors, i.e., no data are processed.",
    },
    "MESSAGES": {
      "Type": ["Mandatory", "Non-repeatable"],
      "Description": "Identifies the warning/error messages file.",
       "Parameters": {
         "message_filename": "The name of the file where all source-code-generated messages are written",
       },
    },
    "REPORT": {
      "Type": ["Optional", "Non-repeatable"],
      "Description": "Identifies the general report file.",
      "Parameters": {
        "summary_filename": "The name of the file where AERMET writes a summary of all preprocessor activity for the current run",
      },
    },
  },
  "UPPERAIR": {
    "Keyword": "UPPERAIR",
    "Type": ["Conditional", "Non-repeatable"],
    "Description": "Start of UPPERAIR pathway.",
    "AUDIT": {
      "Keyword": "AUDIT",
      "Type": ["Optional", "Repeatable"],
      "Description": "Identify variables to be audited. These are in addition to any automatically audited variables.",
      "Parameters": [ 
        {
          "Variable Name": "UAPR",
          "Description": "Atmospheric pressure",
          "Units": "millibars*10",
          "Type": "<",
          "Missing Indicator": "99999",
          "Lower Bound": "5000",
          "Upper Bound": "10999",
        },
        {
          "Variable Name": "UAHT",
          "Description": "Height above ground",
          "Units": "meters",
          "Type": "<=",
          "Missing Indicator": "99999",
          "Lower Bound": "0",
          "Upper Bound": "5000",
        },
        {
          "Variable Name": "UATT",
          "Description": "Dry bulb temperature",
          "Units": "ºC*10",
          "Type": "<",
          "Missing Indicator": "9990",
          "Lower Bound": "350",
          "Upper Bound": "+350",
        },
        {
          "Variable Name": "UATD",
          "Description": "Dew point temperature",
          "Units": "ºC*10",
          "Type": "<",
          "Missing Indicator": "9990",
          "Lower Bound": "350",
          "Upper Bound": "+350",
        },
        {
          "Variable Name": "UAWD",
          "Description": "Wind direction",
          "Units": "degrees from north",
          "Type": "<=",
          "Missing Indicator": "999",
          "Lower Bound": "0",
          "Upper Bound": "360",
        },
        {
          "Variable Name": "UAWS",
          "Description": "Wind speed",
          "Units": "meters/second *10",
          "Type": "<",
          "Missing Indicator": "9990",
          "Lower Bound": "0",
          "Upper Bound": "500",
        },
        {
          "Variable Name": "UASS",
          "Description": "Wind speed shear",
          "Units": "(m/s)/(100 meters)",
          "Type": "<=",
          "Missing Indicator": "9999",
          "Lower Bound": "0",
          "Upper Bound": "5",
        },
        {
          "Variable Name": "UADS",
          "Description": "Wind direction shear",
          "Units": "degrees/(100 meters)",
          "Type": "<=",
          "Missing Indicator": "9999",
          "Lower Bound": "0",
          "Upper Bound": "90",
        },
        {
          "Variable Name": "UALR",
          "Description": "Temperature lapse rate",
          "Units": "ºC/(100 meters)",
          "Type": "<=",
          "Missing Indicator": "9999",
          "Lower Bound": "2",
          "Upper Bound": "5",
        },
        {
          "Variable Name": "UADD",
          "Description": "Dew point deviation",
          "Units": "ºC/(100 meters)",
          "Type": "<=",
          "Missing Indicator": "9999",
          "Lower Bound": "0",
          "Upper Bound": "2",
        },
      ],
    },
    "DATA": {
      "Keyword": "DATA",
      "Type": ["Mandatory", "Non-repeatable", "Reprocessed"],
      "Description": "File name of raw upper air data",
      "Parameters": {
        "archive_filename": "The name of the file containing the archive of upper air data.",
        "file_format": ["6201FB", "6201VB", "FSL"],
      },
    },
    "EXTRACT": {
      "Keyword": "EXTRACT",
      "Type": ["Mandatory", "Non-repeatable"],
      "Description": "File name of extracted upper air data.",
      "Parameters": {
        "extracted_data_filename": "Name of the output file for data extracted from an archive data file and the name of the input file for upper air data QA",
      },
    },
    "LOCATION": {
      "Keyword": "LOCATION",
      "Type": ["Mandatory", "Non-repeatable", "Reprocessed"],
      "Description": "Site ID and location information. Required only for extraction processing.",
      "Parameters": {
        "site_id": "Site identifier for which data are to be processed.",
        "lat(long)": "Station latitude (or longitude) in decimal degrees with the suffix N for sites north of the equator, S for sites south of the equator (or W for sites west of Greenwich, E for sites east of Greenwich).",
        "long(lat)": "Station longitude (or latitude) in decimal degrees with the suffix W for sites west of Greenwich, E for sites east of Greenwich (or N for sites north of the equator, S for sites south of the equator).",
        "[tadjust]": "An integer used to convert the time reported in the database to local Standard time. For standard upper-air data reported in Greenwich Mean Time (GMT), the value is the same as the time zone for the station (e.g., a value of 5 for the Eastern time zone). ",
      },
    },
    "MODIFY": {
      "Keyword": "MODIFY",
      "Type": ["Optional", "Non-repeatable", "Reprocessed"],
      "Description": "Flag indicating corrections should be made to the sounding data when extracted. See '5 for a discussion of these corrections."
    },
    "NO_MISSING": {
      "Keyword": "NO_MISSING",
      "Type": ["Optional", "Repeatable"],
      "Description": "Identifies those variables to QA and summarize the messages only; detailed message identifying the violation and date is suppressed.",
      "Parameters": {
        "uaname1 ... uanameN": "Suppresses missing data messages for the upper air variables specified, as defined in Appendix B; the number of times the variable is missing is not tallied.",
      },
    },
    "QAOUT": {
      "Keyword": "QAOUT",
      "Type": ["Mandatory", "Non-repeatable"],
      "Description": "File name of upper air data for quality assessed output/merge input.",
      "Parameters": {
        "qa_output_filename": "Name of the output file from the QA/input to merge data.",
      },
    },
    "RANGE": {
      "Keyword": "RANGE",
      "Type": ["Optional", "Repeatable", "Reprocessed"],
      "Description": "Set new upper and lower bounds and missing values for QA of the variable listed.",
      "Parameters": {
        "uaname": ["UAPR", "UAHT", "UATT", "UATD", "UAWD", "UAWS", "UASS", "UADS", "UALR", "UADD"],
        "lower_bound": "Minimum value of the valid range of values for uaname",
        "<[=]": "Exclude (<) or include (<=) the lower and upper bounds (the endpoints) in the QA",
        "upper_bound": "Maximum value of the valid range of values for uaname",
        "missing_indicator": "Value to indicate the value is missing",
      },
    },
    "XDATES": {
      "Keyword": "XDATES",
      "Type": ["Mandatory", "Non-repeatable"],
      "Description": "Inclusive dates identifying the period of time to extract from the archive data file.",
      "Parameters": {
        "YB/MB/DB": "Beginning year, month and day to extract; the slash (/) between each part of the date field is required; there can be no blanks in this parameter",
        "[TO]": "Optional; used to make this record more readable",
        "YE/ME/DE": "Ending year, month and day to extract; the slash (/) between each part of the date field is required; there can be no blanks in this parameter",
      },
    },
  },
  "SURFACE": {},
  "ONSITE": {},
  "MERGE": {},
  "METPREP": {},
}
```

<!--
=====================================================================
-->
