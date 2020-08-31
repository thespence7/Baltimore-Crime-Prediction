# Predicting Crime in Baltimore
Using machine learning to forecast the Total Crime in Baltimore.

## Why Crime in Baltimore?
Ever since watching HBO's The Wire, I have been fascinated with Baltimore crime. Crime effects not only the state of one's city, h

Beginning with the opinion of West v. Barnes in 1791, the Court has defended the Constitution and American people for over 200 years. Decisions made in this Court have long-lasting implications that affect hundreds of millions of people. As someone who follows politics and the Court I decided that attempting to predict outcomes of cases would be a good exercise in using NLP while still finding the topic interesting. Baltimore Police Department's Crime Dataset (1957-2020)

## Data Acquisition
__Transcripts__:
    I sourced the crime data from Baltimore Police Department's [crime database](https://data.baltimorecity.gov/Public-Safety/BPD-Part-1-Victim-Based-Crime-Data/wsfq-mvij). The data was originally provided by Oyez, an "unofficial online multimedia archive of the Supreme Court of the United States". Each file corresponds to one case formatted in JSON, containing relevant case information (docket, term, decision data, etc...) and the transcript of the oral argument.

Weekly-Trend-Graph:
![Alt text](images/UpdatedWeeklyTrendGraph.png)

The Crime data I started with was CSV formatted which was perfect for particularly useful in this case. For each case I extracted relevant case information (docket, term, decision date, etc...) and the transcript of the oral arguments, and inserted it into a CSV file. The transcripts are broken up into portions depending on who is speaking. To start, I decided to make each portion its own row in the CSV. This is the [transcripts_by_justice.csv](https://github.com/rcohngru/Predicting-Supreme-Court-Outcomes/blob/master/data/transcripts_by_justice.csv) file.

I then created CSV files for each justice where each row corresponds to a unique case. I concatenated all of the separate speaking moments for each case, so each row contains a document representing every word the justice spoke during the oral arguments. Conveniently, the Oyez dataset also contains pre-cleaned versions of the transcripts meaning that I do not have to bother with it.

Finally, I joined the justice CSVs with the decisions data from Washington University. Interestingly, the Washington University did not contain explicit data for how each justice voted--rather the data it contained was if the justice voted with the majority, and if the petitioning party won the case. I converted this data into a vote column using the following schema.


![SARIMAX](images/
