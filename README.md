Overview of the analysis:

The purpose of this week’s analysis is to connect to a SQLite database and then pull queries from the database using SQLAlchemy.  From then we are aiming to filter the temperature data and then transform it into a pandas dataFrame, and ending with our summary statistics this was done for the months of June and December.

Results:
•	Deliverable 1:
1.	During the month of June, the lowest temperature that was reached was 64 degrees Fahrenheit.  This was of 1700 data points.
2.	During the month of June, the highest temperature that was reached was 85 degrees Fahrenheit.  This was of 1700 data points.
3.	The average temperature in June, is approximately 75 degrees Fahrenheit when rounding to the nearest whole integer.
See image below
![This is an image](https://github.com/BMoreland20/Surfs_Up/blob/main/Resources/June%20Temps.png)


•	Deliverable 2:
1.	During the month of December, the lowest temperature that was reached was 56 degrees Fahrenheit.  This was of 1517 data points.
2.	During the month of December, the highest temperature that was reached was 83 degrees Fahrenheit.  This was of 1517 data points.
3.	The average temperature in December, is approximately 71 degrees Fahrenheit when rounding to the nearest whole integer.
See image below
![This is an image](https://github.com/BMoreland20/Surfs_Up/blob/main/Resources/December%20Temps.png)

Summary:

The month of June has an average temperature of 75 degrees Fahrenheit with a December average of 71 degrees Fahrenheit.  From these results either month could be very viable time to surf.  However, it should be noted that in December you could drop down to 56 degrees which would be less than ideal temperature to surf in.  While in June the lowest temperature drop came down to 64 degrees, which would be more ideal weather to surf than that of December.

With this said going strictly off of temperature is not enough, we would also want to look a precipitation for June and December as well to get a fuller picture.  The two sqlalchemy queries and code to create dataframes and descriptive stats will show a way to obtain this information.
Base query for June:
`columns = [Measurement.date, Measurement.prcp,]
june_precip = (session.query(*columns)
    .filter(func.strftime("%m", Measurement.date) == "06")
)`

Set up and print dataframe:
`june_df = pd.DataFrame(june_prcp, columns=['date','prcp'])
june_df.set_index(june_df['date'], inplace=True)
june_df = june_df.sort_index()
print(june_df.to_string(index=False))`

Run descriptive stats:
` june_df.describe()`


Base query for December:
` columns = [Measurement.date, Measurement.prcp,]
dec_prcp = session.query(*columns).\
    filter(func.strftime("%m", Measurement.date) == "12") `

Set up and print dataframe:
` dec_df = pd.DataFrame(dec_prcp, columns=['date','prcp'])
dec_df.set_index(dec_df['date'], inplace=True)
dec_df = dec_df.sort_index()
print(dec_df.to_string(index=False)) `

Run descriptive stats:
` dec_df.describe()`

From this data we now have a better understanding of the weather in the two months in question.  All be it the averages between the two months has a small difference, by doing a quick Welch’s t-test of independence and an alpha value of .05 we can determine that the means are not statistically significant.  This test can be performed by utilizing the following code.
` res = ttest_ind(v1, v2, equal_var= False)
print(res) `
