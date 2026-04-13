# 📊 **U.S. Flight Delay Analysis**

This project has two main objectives:
1. Analyze the key factors contributing to flight delays in 2024.
2. Forecast the number of delayed flights for each month from January to July 2025.

# 📌 **Overview**

This project will cover the following:
- Conduct a high-level analysis of flights delayed in the U.S. in 2024.
- Assess factors contributing to flights getting delayed in the U.S. in 2024.
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

The above chart clearly illustrates that while Morning, Afternoon, Evening, and Midnight hours cover exactly the same number of hours (~6 hrs), Morning and Afternoon flights each account to 36% and 35% of the total flights respectively in 2024 with Evening (~23%) and Midnight flights (~5%) being a distant #3 and #4 respectively in terms of flight distribution. This shows that majority Americans prefer travelling domestically during daylight hours.

Flight volumes follow a clear seasonal pattern. The year starts quietly (January ~560k, February ~550k — the lowest month), builds through spring, peaks in summer (July at ~660k — the busiest month), eases through autumn, and dips again in November (~605k) before a mild December recovery. Summer demand is roughly 20% higher than the winter low.

**Chart 2: Number of Flights by Month — On Time vs. Delayed**

Note: Based on industry standards, any flight that departs more than 15 minutes after its scheduled departure time is counted as a delayed flight.

<img width="1152" height="544" alt="image" src="https://github.com/user-attachments/assets/761d32c4-0ad8-4904-ad13-44cf37dcbdda" />

The above chart illustrates that while number of charts throughout the year largely remain uniform, delay rates start moderately in January (22%), improve sharply in February (15%), then gradually worsen through spring into a summer peak of 28% in July — meaning almost 3 in 10 flights were delayed that month. Rates then recover strongly through autumn, bottoming out at 13% in October, before deteriorating again into December (21%). 

Two months stand out as anomalies worth noting. February has both the lowest total volume and a surprisingly low delay rate (15%) for a winter month, suggesting it escapes the typical weather disruption that hits January. September–November form a sustained "golden window" of punctuality, with delay rates of 14%, 13%, and 14% respectively. October's 87% on-time rate is the annual best.

In conclusion, delay rate is not affected by the volume of flights in a month but rather seasonal peaks. In the U.S., summer period peaks in July which coincides with Fourth of July holiday week leading to a spike in domestic travel. Likewise, winter period peaks in late-December and early-January which coincides with Christmas and New Year holiday weeks leading to another spike in domestic travel.

**Chart 3: Delayed Flights by Month with Time-of-Day Breakdown and Average Delay Duration**

<img width="1440" height="671" alt="image" src="https://github.com/user-attachments/assets/eacd16cd-924a-4a08-afd3-f26184326d5c" />

The above chart illustrates that:

- Like Chart 2, Chart 3 also establishes that the volume of delayed flights follow a strong seasonal pattern. The May–July window is clearly the most disrupted period with July peaking at roughly 185,000 delayed flights, nearly 2.3 times the February low of ~80,000. Autumn (September–November) provides sustained relief, with all three months sitting around 84,000–87,000 delayed flights — the best of the year. December then spikes back up to ~128,000, reflecting the return of winter disruption.
- A rather surprising finding from the above chart is the distribution of delayed flights by Time-of-day. For instance, although Chart 1 established that Morning hrs flights accounted to 36% of the total flights in 2024, Chart 3 showed that they accounted to only 20% of the total delayed flights that year. On the other hand, while Evening hrs flights only accounted to 23% of the total flights in 2024 (based on Chart 1), they accounted to 39% of the total delayed flights that year (based on Chart 3). This concludes that Evening hrs flights were relatively the most inefficient in terms of being on time in 2024.
- The average delay duration trend clearly illustrates a strong positive correlation (+0.92) between the number of flights delayed in a month and the monthly average delay in minutes. In other words, greater the number of delayed flights in a month, higher would be the average delay in minutes. 

**Chart 4: Delayed Flights by Time-of-Day (with On-Time vs. Delayed breakdown) and Average Delay Duration**

<img width="1013" height="541" alt="image" src="https://github.com/user-attachments/assets/3f766a54-7723-4fa3-8be7-1fb25b3a9e41" />

The above chart illustrates that:
- In terms of the proportion of delayed flights, Evening Hrs flights are the most inefficient since 33% of their flights were delayed in 2024. Therefore, this finding corroborates one of the findings of Chart 3.
- In terms of average delay duration (in minutes), Midnight Hrs flights are the most inefficient because on average, they are delayed by 144 minutes (2 hrs and 24 mins), which is nearly 2 times the delay rate of Morning, Afternoon, and Evening Hrs flights.

**Chart 5: Top 35 Airport Origins by Number of Delayed Flights**

Context: The reason behind analyzing only the top 35 airports (by origins) and not all airports was that approximately 70% of the total flights delayed in 2024 came from these top 35 airports.

<img width="1121" height="594" alt="image" src="https://github.com/user-attachments/assets/3f293022-e16c-44d4-9520-24f11f789383" />

The above chart illustrates that:
- **DFW is in a league of its own.** Dallas/Fort Worth originates roughly 82,000 delayed flights in 2024 — meaningfully ahead of the next tier of Denver (DEN, ~69,500), Chicago O'Hare (ORD, ~65,500), Charlotte (CLT, ~60,000) and Atlanta (ATL, ~59,000). These five airports form a clear top tier, all major hub-and-spoke hubs with enormous connecting traffic. Their sheer volume of operations makes them naturally susceptible to delay accumulation.
- **Volume and mean don't have a statistically meaningful correlation.** The red line does not follow the bars — it moves independently, which is the most important structural insight in this chart. SEA (Seattle) and DCA (Washington Reagan) both have moderate delay volumes (~34,500 and ~26,000 respectively) but post two of the lowest mean delays on the chart (~56 minutes each). Conversely, MCO (Orlando), IAH (Houston Intercontinental), and STL (St. Louis) show relatively high mean delays despite sitting in the lower half of the volume ranking. This tells us that being a busy origin does not necessarily mean your delays are long — and a quieter airport can still punish passengers with lengthy waits when disruptions do occur.

**Chart 6: Top 35 Airport Destinations by Number of Delayed Flights**

Context: The reason behind analyzing only the top 35 airports (by destination) and not all airports was that approximately 70% of the total flights delayed in 2024 came from these top 35 airports.

<img width="1095" height="608" alt="image" src="https://github.com/user-attachments/assets/de8a48f1-7f41-4957-b21b-0f0c49fde7ea" />

The above chart illustrates that:
- **The destination ranking mirrors origins closely, but with lower volumes.** DFW again leads (~68,000 delayed arrivals), followed by ATL, DEN, and ORD in a tight cluster (~56,000–57,500 each). The same major hub airports dominate — unsurprising, since the busiest origin airports are also the busiest destinations. However, the volumes are consistently lower than on the origins chart, which reflects the fact that delays accumulated in flight can sometimes be partially recovered before landing.
- **Mean delay durations are higher and more volatile at destinations than at origins.** This is the most striking difference between the two charts. Where origin mean delays ranged roughly from 56 to 88 minutes, destination mean delays are elevated across the board and spike more dramatically. DFW stands out with a mean arrival delay of ~96 minutes — the highest of any airport in either chart. DEN, ORD, LGA, EWR, DCA, and JFK all cluster around 88–90 minutes. This makes intuitive sense: arrival delays compound. A flight that departs late, encounters en-route issues, or arrives into a congested airport stacks multiple delay sources on top of each other, pushing the average duration higher than at the point of origin.

Another interesting finding upon reading Charts 5 and 6 together is that with the exception of MSY (New Orleans), the same airports appear in both top 35 lists, confirming that delay risk is structurally concentrated at a handful of major hubs — DFW, DEN, ORD, ATL, and CLT. These airports generate and receive the most delayed flights simply because they handle the most total traffic and act as connection points where delays propagate across the network.
