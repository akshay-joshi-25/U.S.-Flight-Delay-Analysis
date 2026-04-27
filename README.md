# 📊 **U.S. Flight Delay Analysis**

This project has two main objectives:
1. Conduct Exploratory Data Analysis on 2024 Flight Delay data.
2. Forecast the number of delayed flights for each month from January 2025 to July 2025 using historical data (Jan 2022 to Dec 2024).

# 📌 **Overview**

This project will cover the following:
- Conduct a high-level analysis of flights delayed in the U.S. in 2024.
- Forecast the number of flights that will be delayed in the first half of 2025 using a Time Series model.
- Compare the predictions with the actuals to evaluate model accuracy.

# 📂 **Datasets**
The dataset used for this project were publicly made available by the Bureau of Transportation Statistics from 2022 to 2025. 
- It contained 26.3 million rows, each row representing a domestic flight in the U.S. that departed anytime between Jan 1, 2022 and July 31, 2025.
- Columns include departing and arriving airports, airline, flight number, scheduled departure, minutes flight delayed, and flight cancelled.

You can access this dataset (via Row Zero) by clicking [here](https://rowzero.com/datasets/us-flights-dataset).

# 🔧 **Tools Used**

- **Python** was used for time series forecasting.
- **Excel** was used for data visualization and exploratory data analysis.

# 📈 **High-Level Analysis**

**Chart 1: Number of Flights by Month with Time-of-Day Breakdown**

Note:
- Morning Hrs - consists of all flights that depart anytime between **06:00 and 11:59.**
- Afternoon Hrs - consists of all flights that depart anytime between **12:00 and 17:59.**
- Evening Hrs - consists of all flights that depart anytime between **18:00 and 23:59.**
- Midnight Hrs - consists of all flights that depart anytime between **00:00 and 05:59.**

Therefore each time-of-day covers ~6 hours.

<img width="1373" height="560" alt="image" src="https://github.com/user-attachments/assets/f8364989-97c0-4d44-b555-f562e1d195dd" />

The above chart clearly illustrates that while Morning, Afternoon, Evening, and Midnight hours cover exactly the same number of hours (~6 hrs), Morning and Afternoon flights each account to 36% and 35% of the total flights respectively in 2024 with Evening (~23%) and Midnight flights (~5%) being a distant #3 and #4. This shows that majority Americans prefer travelling domestically during daylight hours.

Flight volumes, though largely uniform end up following a clear seasonal pattern. The year starts quietly (January ~560k, February ~550k — the lowest month), builds through spring, peaks in summer (July at ~660k — the busiest month), eases through autumn, and dips again in November (~605k) before a mild December recovery. Summer demand is roughly 20% higher than the winter low.

**Chart 2: Delayed Flights by Month with Time-of-Day Breakdown and Average Delay Duration**

Note: Based on industry standards, a flight is considered to be delayed if it departs more than 15 minutes after its scheduled departure time.

<img width="1440" height="671" alt="image" src="https://github.com/user-attachments/assets/eacd16cd-924a-4a08-afd3-f26184326d5c" />

The above chart illustrates that:

- While the volume of flights throughout the year remain largely uniform (Chart 1), the volume of delayed flights follow a strong seasonal pattern. The May–July window is clearly the most disrupted period with July peaking at roughly 185,000 delayed flights, nearly 2.3 times the February low of ~80,000. Autumn (September–November) provides sustained relief, with all three months sitting around 84,000–87,000 delayed flights — the best of the year. December then spikes back up to ~128,000, reflecting the return of winter disruption.
- This shows that the delay rate is not affected by the monthly volume of flights, but rather by seasonal factors. In the U.S., the summer season peaks in July, which coincides with the Fourth of July holiday week and leads to a spike in both domestic and international travel, resulting in busier air traffic. Similarly, the winter period peaks in late December and early January, which coincides with the Christmas and New Year holiday season, leading to another surge in domestic and international travel.
- A rather surprising finding from the above chart is the distribution of delayed flights by Time-of-day. For instance, although Chart 1 established that Morning hrs flights accounted to 36% of the total flights in 2024, Chart 3 showed that they accounted to only 20% of the total delayed flights that year. On the other hand, while Evening hrs flights only accounted to 23% of the total flights in 2024 (based on Chart 1), they accounted to 39% of the total delayed flights that year (based on Chart 3). This concludes that Evening hrs flights were relatively the most inefficient in terms of being on time in 2024.
- The average delay duration trend clearly illustrates a strong positive correlation (+0.92) between the number of flights delayed in a month and the monthly average delay in minutes. In other words, greater the number of delayed flights in a month, higher would be the average delay in minutes. 

# 🧠 **Forecasting Flight Delay using Time Series Model**

**Chart 4: Volume of Delayed Flights (Jan 2022 to Dec 2024)**

<img width="1184" height="618" alt="image" src="https://github.com/user-attachments/assets/bbd2c446-6b71-47c2-883b-12253ef4c617" />

Three clear patterns emerge from this time series.
- **Consistent seasonality.** Every single year follows the same rhythm: delays climb into a summer peak (June–July), fall back through autumn to a trough around September–October, briefly spike in December, then dip again in February. This seasonal heartbeat repeats reliably across all three years and confirms what the earlier charts showed for 2024 alone.
- **A worsening multi-year trend.** The peaks are getting higher year on year. The summer 2022 peak reached roughly 140,000 delayed flights; summer 2023 surged to ~175,000; and summer 2024 hit a new high of ~185,000. The troughs are also drifting upward — the autumn 2023 low (~78,000) was lower than autumn 2024 (~82,000), but the general floor of the series is rising. The network is handling more total flights and accumulating more delays over time.
- **2023 was the most disrupted year overall.** Not only did July 2023 post the highest single month until that point, but the entire mid-year period (May–August 2023) was elevated. 2024 then broke the July record but showed a notably sharper and deeper autumn recovery, with September–November 2024 forming the cleanest low period across the whole series.

The above time series yielded a p-value of 0.000005 (≈ 5.11 × 10⁻⁶) and an ADF Statistic of -5.314, strongly indicating that the data is stationary (i.e., it behaves consistently over time) making it suitable for forecasting using SARIMA models.

**Chart 5: Model Diagnostics of SARIMA Order (0,1,0)**

<img width="311" height="213" alt="image" src="https://github.com/user-attachments/assets/6d6e9255-d854-4370-9899-2911b989cf64" />

There are four diagnostic panels here, each testing a different assumption. Together they paint a clear picture of model quality.

**Top-left — Standardised Residuals**
The residuals fluctuate around zero without any obvious drift, trend, or growing variance over time. There are a couple of spikes (notably one reaching above 2 and one below -2) but nothing extreme enough to be alarming. This is broadly healthy — the model is not systematically over- or under-predicting across the series.

**Top-right — Histogram + Estimated Density**
The histogram of residuals is compared against a standard Normal N(0,1) curve (green) and a KDE of the actual residuals (orange). The residuals are reasonably bell-shaped and centred near zero, though there is a slight right skew and the distribution is a little narrower than the theoretical normal. This suggests near-normality, which is acceptable for forecasting purposes, though not perfect.

**Bottom-left — Q-Q Plot**
This is the strongest panel in the diagnostic. The sample quantiles track the red theoretical line very closely across almost the entire range, with only mild deviation at the upper tail (the top two points drift slightly right). This is a good result — it confirms that residuals are approximately normally distributed, which validates the model's statistical inference and confidence intervals.

**Bottom-right — Correlogram (ACF of Residuals)**
All autocorrelation bars fall well within the shaded confidence band (approximately ±0.35) at every lag from 1 to 10. There is no lag where the residuals show significant autocorrelation. This is the key test for a time series model — it confirms that the SARIMA specification has successfully captured the temporal structure in the data, leaving behind white noise residuals. Nothing systematic remains unexplained.

Since the model diagnostics showed that the above SARIMA model is well fitted, we will use it to predict delayed flights between Jan 2025 and July 2025 and compare it with the actuals.

**Chart 6: Actuals vs. Predictions Comparison**

<img width="836" height="182" alt="image" src="https://github.com/user-attachments/assets/e3f20a28-a716-4303-ad6a-25abf2ecce65" />

The SARIMA model has an adjusted R² of 0.78 on seven out-of-sample points, indicating a reasonable fit. The model is directionally sound — it correctly anticipates the upward trend from spring into peak summer — but it struggles at the inflection points: the winter trough transition and the steepness of the summer acceleration. 

January and February are the most problematic months and in opposite directions. The model over-predicts January by 22,251 flights — the largest single error in the table and the biggest contributor to SS_res. It then under-predicts February by 17,800. These back-to-back large errors in opposite directions suggest the model misread the timing of the post-New Year dip, expecting the trough to arrive later than it did. The chart confirms this: the dashed predicted line sits visibly above the actual in January, then dips below it in February.

March through May are the model's best months by some distance. Errors of -6,633, -2,476 and +3,969 are tight, and the predicted line tracks the actual closely on the chart through this window. The model has a solid grasp of the spring volume pattern.

June is the second largest absolute error at 20,001 flights under-predicted. The actual line accelerates sharply upward into summer while the predicted line rises more gradually — the model underestimates the speed and magnitude of the summer ramp. This is a direct consequence of the escalating peak pattern identified in the historical time series: a model trained on earlier, lower peaks will structurally under-forecast a summer that breaks previous records.

July nearly self-corrects, with an error of just 1,901. By the time the series reaches its July plateau, the model converges well — suggesting it knows roughly where the summer ceiling is, even if it misjudges the climb to get there.

You can access the Python code used to build the SARIMA model and make predictions by clicking [here.](https://github.com/akshay-joshi-25/U.S.-Flight-Delay-Analysis/blob/main/Time%20Series%20Modelling.ipynb)

To access the CSV file used to train the SARIMA model, click [here.](https://github.com/akshay-joshi-25/U.S.-Flight-Delay-Analysis/blob/main/Delayed%20Flights.csv)
