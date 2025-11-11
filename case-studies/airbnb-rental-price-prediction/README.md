# Problem Statement: Airbnb Rental Price Prediction

## Context

Airbnb has revolutionized the short-term rental industry by providing a platform that connects property owners with travelers seeking accommodation. From single-room listings by individual hosts to large-scale property management firms handling multiple units, Airbnb offers diverse options to meet various customer needs. The company operates on a commission-based revenue model, earning 6-12% of the booking fee from guests and 3% from hosts per successful transaction.

With an ever-growing number of listings, setting the right rental price is a complex challenge. Hosts need to optimize their pricing strategies to maximize occupancy and increase revenue, while travelers seek fair and competitive pricing that aligns with their expectations. Airbnb itself must ensure that the pricing structure remains attractive to both parties while maintaining its market competitiveness. Factors such as room type, number of bedrooms, review scores, cancellation policies, and instant booking availability significantly influence rental pricing, making manual price adjustments inefficient and error-prone.

To address these challenges, Airbnb has taken a data-driven approach to create a dynamic pricing strategy. By leveraging historical rental data, the company identifies pricing patterns using a predictive model that assists hosts in setting optimal rental prices. This not only enhances business profitability but also improves customer experience by ensuring fair pricing across the platform.

## Objective

As a Data Scientist at Airbnb, you need to scale the machine learning model that predicts the rental price of a property based on its features. The objective is to deploy this pricing model into a user-friendly web application, allowing Airbnb hosts and internal teams to input property details and obtain accurate rental price predictions instantly. This will enable Airbnb and its stakeholders to:

- Improve Pricing Strategies: By predicting rental prices accurately, hosts can adjust their listings to attract more bookings while maximizing earnings.
- Enhance Market Competitiveness: A well-calibrated pricing model ensures that Airbnb remains competitive compared to hotels and other rental platforms.
- Provide Actionable Insights: The model will highlight key factors influencing rental prices, allowing Airbnb to refine its pricing recommendations.
- Enable Real-Time Predictions: By deploying the model as a web application, Airbnb can offer instant price suggestions to hosts, enabling data-driven decision-making in real time.
- Successful implementation will enhance revenue generation, improve host satisfaction, and provide customers with fair rental pricing options across the platform.

## Data Description

The data contains information about the different types of rental rooms offered by Airbnb over a fixed period of time. The detailed data dictionary is given below.

- **id:** Property ID
- **room_type:** Type of Room in the property
- **accommodates:** How many adults can this property accommodate
- **bathrooms:** Number of bathrooms on the property
- **cancellation_policy:** Cancellation policy of the property
- **cleaning_fee:** This denotes whether the property cleaning fee is included in the rent or not
- **instant_bookable:** It indicates whether an instant booking facility is available or not
- **review_scores_rating:** Review rating score of the property
- **bedrooms:** Number of bedrooms in the property
- **beds:** Total number of beds in the property
- **log_price:** Log of the rental price of the property for a fixed period. [If the price is 12000 dollars, then log_price represents log(12000)]
