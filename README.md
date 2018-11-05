
# Top 10 AWR Baselines

Here's a method to find the periods of top activity in AWR and create a baseline for the top 10 periods.

The baseline can be made to expire after a set number of days so that you can just set them and forget them.

Use a reasonable value (30 days?) after which the baselines will just expire.

Be sure to allow enough time to ensure you will be done with them.

This code looks for the top 10 AAS (Average Active Sessions) periods and creates a baseline for each.

The same idea could be used to find top PGA usage, CPU, IO, etc.

## Files

### top10.sql

This is a script fragment that is called from create-awr-baselines.sql.

Its purpose is to find the top 10 AWR Snapshots in terms of maximum AAS (Average Active Sessions)

### create-awr-baselines.sql

This script creates AWR baselines based on the findings from top10aas.sql.

The baselines will be named with a prefix of _AWR-Top10_

The retention period is set by the sqlplus variable _:n_expire_days_, and is currently set to 1 day

The call to top10aas.sql could be replaced with any similar SQL fragment that finds the top N snap_id's based on PGA usage, IO, etc.

This script will also genereate the SQL script _top10-awrrpt.sql_ which can be used to generate an AWR report for each of the baselines.

These AWR reports are instance specific, so on a RAC system the report will be generated for the specific instance where the top db activity was found.

### show-awr-baselines.sql

Displays entries in DBA_HIST_BASELINE

### drop-awr-baseline.sql

This script drops all baselines named with a prefix of  _AWR-Top10_

### aas-[123].sql

Examples of different methods that may be used to determine the top 10 AWR snapshots to examine.

## Test Run

As shown these baselines were all created during a previous execution of the script

```sql

SQL> @create-awr-baselines

==============================
begin_time: 21-JUL-16 10.00.48.352 PM
begin snap_id: 4511
end snap_id: 4512
AAS: 9.96505830418124
Baseline Name: dw-tuning_4511_20160721-22:00:48
!!Baseline dw-tuning_4511_20160721-22:00:48 already exists
==============================
begin_time: 20-JUL-16 10.00.11.550 PM
begin snap_id: 4487
end snap_id: 4488
AAS: 9.1440137816245
Baseline Name: dw-tuning_4487_20160720-22:00:11
!!Baseline dw-tuning_4487_20160720-22:00:11 already exists
==============================
begin_time: 27-JUL-16 10.00.29.465 PM
begin snap_id: 4655
end snap_id: 4656
AAS: 9.05557091726319
Baseline Name: dw-tuning_4655_20160727-22:00:29
!!Baseline dw-tuning_4655_20160727-22:00:29 already exists
==============================
begin_time: 25-JUL-16 10.00.33.624 PM
begin snap_id: 4607
end snap_id: 4608
AAS: 8.25054401332223
Baseline Name: dw-tuning_4607_20160725-22:00:33
!!Baseline dw-tuning_4607_20160725-22:00:33 already exists
==============================
begin_time: 22-JUL-16 10.00.15.373 PM
begin snap_id: 4535
end snap_id: 4536
AAS: 7.57279970034959
Baseline Name: dw-tuning_4535_20160722-22:00:15
!!Baseline dw-tuning_4535_20160722-22:00:15 already exists
==============================
begin_time: 24-JUL-16 06.00.36.164 AM
begin snap_id: 4567
end snap_id: 4568
AAS: 7.4487293040293
Baseline Name: dw-tuning_4567_20160724-06:00:36
!!Baseline dw-tuning_4567_20160724-06:00:36 already exists
==============================
begin_time: 23-JUL-16 06.00.06.736 AM
begin snap_id: 4543
end snap_id: 4544
AAS: 6.71252810261536
Baseline Name: dw-tuning_4543_20160723-06:00:06
!!Baseline dw-tuning_4543_20160723-06:00:06 already exists
==============================
begin_time: 26-JUL-16 10.00.58.588 PM
begin snap_id: 4631
end snap_id: 4632
AAS: 6.31525476507831
Baseline Name: dw-tuning_4631_20160726-22:00:58
!!Baseline dw-tuning_4631_20160726-22:00:58 already exists
==============================
begin_time: 23-JUL-16 11.00.50.872 PM
begin snap_id: 4560
end snap_id: 4561
AAS: 4.02516348043297
Baseline Name: dw-tuning_4560_20160723-23:00:50
!!Baseline dw-tuning_4560_20160723-23:00:50 already exists
==============================
begin_time: 25-JUL-16 09.00.28.448 PM
begin snap_id: 4606
end snap_id: 4607
AAS: 3.83920206563385
Baseline Name: dw-tuning_4606_20160725-21:00:28
!!Baseline dw-tuning_4606_20160725-21:00:28 already exists
==============================
```


