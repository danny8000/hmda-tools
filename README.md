hmda_tools
==========

Tools to make analyzing HMDA data much easier.

* `bin/`: Scripts to load data.  
  * `bin/hmda_load_cbsa`: Download and load the Dec 2009 CBSA data, allowing you to the `msa_md` column from HMDA with a Metropolitian Statistical Area (MSA).
  * `bin/load_state_county.py`: Download and load the 2010 Census Gazetteer data, allowing you to associate state and county FIPS codes from HMDA to names and demographic data.
* `code_sheet/`: CSV files containing all the lookup tables from the
  HMDA code sheets for 2010 and 2011.
* `code_sheet.postgres.sql`: The lookup tables from the `code_sheet/`
  directory as a Postgres dump.

How to download and load HMDA data
----------------------------------
The following commands will load the 2011 HMDA data into MySQL. Please feel free to contribute a better automated way to work with multiple DBs.

```sh
wget http://www.ffiec.gov/hmdarawdata/LAR/National/2011HMDALAR%20-%20National.zip -O hmda11.zip
unzip -p hmda11.zip | sed 's/NA//g' | sed 's/ //g' > hmd11c.csv
mysql -e 'load data local infile 'hmda11c.csv' into table hmda fields terminated by ',' lines terminated by "\n";'
```

Schema:

```sql
CREATE TABLE hmda
(year integer,
respondent char(10),
agency integer,
loan_type integer,
property_type integer,
loan_purpose integer,
occupancy integer,
 loan_amount integer,
preapproval integer,
action_type integer,
msa_md integer,
state_code integer,
county_code integer,
census_tract_number char(8),
applicant_ethnicity integer,
co_applicant_ethnicity integer,
applicant_race_1 integer,
applicant_race_2 integer,
applicant_race_3 integer,
applicant_race_4 integer,
applicant_race_5 integer,
co_applicant_race_1 integer,
co_applicant_race_2 integer,
co_applicant_race_3 integer,
co_applicant_race_4 integer,
co_applicant_race_5 integer,
applicant_sex integer,
co_applicant_sex integer,
 applicant_income integer,
purchaser_type integer,
denial_reason_1 integer,
denial_reason_2 integer,
denial_reason_3 integer,
rate_spread varchar(10),
hoepa_status integer,
lien_status integer,
edit_status integer,
sequence_number integer,
population integer,
minority_population double precision,
hud_median_family_income integer,
tract_to_msa double precision,
number_of_owner_occupied_units integer,
number_of_family_units integer,
application_date_indicator integer);
```


Current Needs
-------------
* MSA codes in CSV/SQL format (http://www.census.gov/population/metro/files/lists/2009/List1.txt)


Public Domain
--------------

<p xmlns:dct="http://purl.org/dc/terms/" xmlns:vcard="http://www.w3.org/2001/vcard-rdf/3.0#">
  <a rel="license"
     href="http://creativecommons.org/publicdomain/zero/1.0/">
    <img src="http://i.creativecommons.org/p/zero/1.0/88x31.png" style="border-style: none;" alt="CC0" />
  </a>
  <br />
  To the extent possible under law,
  <a rel="dct:publisher"
     href="http://github.com/crnixon/hmda_tools">
    <span property="dct:title">Clinton Dreisbach</span></a>
  has waived all copyright and related or neighboring rights to
  <span property="dct:title">hmda_tools</span>.
This work is published from:
<span property="vcard:Country" datatype="dct:ISO3166"
      content="US" about="http://github.com/crnixon/hmda_tools">
  United States</span>.
</p>
