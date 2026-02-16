## Inventory Forecasting and Par Level Optimization

1. What is the core business problem and why does it matter?
    The hotel chain manages the different locations through different bars and it has a repetitive inventory problem. Certain products with high demand will often experience shortages thus missing their sales and angering their customers. Meanwhile, low-moving products tend to be stocked in excess, and this occupies capital and inflates the storage costs and, in some cases, leads to wastage or spoilage.

    Stockouts as well as overstocking impacts profitability and customer satisfaction directly. The existing inventory decisions are mostly through the use of a manual judgment or fixed rule that fails to respond to the evolving demand patterns like weekends, seasonality, or special events.

    The fundamental aim of the project is to develop a data-driven piece that will predict the demand at the item level and suggest the best inventory levels (par levels). This assists the managers in keeping an adequate inventory at the minimal cost possible and results into wiser and more consistent operation decision making.
2. What assumptions did you make? Why?
    A number of simplifying assumptions were done to render the problem tractable and to model a realistic system.

    The demand is supposed to be forecastable based on the previous consumption patterns. The supplier lead time is set to be constant (two days). The treatments of an item and location are performed separately. There are no assumptions made about the cost of holding and stockout cost. The assumption made is that replenishment is done as soon as the inventory becomes lower than the reorder point. There are no supply chain break ins and lagging.

    These are the assumptions which give us the chance to concentrate on the accuracy of the forecasts and optimization of the inventory without introducing any extra dimensions. In a real deployment, these values may be substituted with real operational data of the hotel.
3. What model did you use and why did you choose it? Why not others?
    The forecasting model applied in this project is LightGBM, which is a gradient boosting decision tree model.

    LightGBM was selected as it works very well with structured tabular data, and it is able to capture non-linear relationships, and it is able to train fast and scale efficiently to many items and locations. It is also compatible with engineered time based functions like lag demand and rolling averages.

    More basic baselines such as moving averages were also taken into consideration but they fail to capture seasonality or complicated patterns. Statistical models such as ARIMA/SARIMA are more difficult to scale to hundreds of products and they need to be tuned individually on a per-item basis. LSTMs and other deep learning methods were not used since they are complex and increase the amount of data needed, and they do not offer much added value to this style of tabular time series problem.
4. How does your system perform? What would you improve?
    The standard practices of measuring performance included MAE and RMSE. The model was able to reflect the weekly seasonality and overall general demand trend of most items.

    An inventory simulation was constructed to assess the impact of business. The simulation measured holding cost, cost of stockout and the number of stockouts. The forecast-based par levels minimised stockouts and decreased the total costs as opposed to a naive or fixed inventory approach.

    There is a number of improvement opportunities. Other characteristics like holidays, promotions, or events would be useful in enhancing forecasts. Fast moving and slow moving products could be handled in different ways. Accuracy could be further enhanced by hyperparameter tuning. The system could also be more robust by applying probabilistic forecasting and modeling variability of suppliers.
5. How would this solution work in a real hotel?
    In practice, the system would be automatic and would be part of the day to day operations. The consumption data of the previous day would be taken every night. The model would also predict the demand within the coming few days and calculate the recommended par levels by item in each location. Such suggestions would be presented in a dashboard or they would be exported as an order list to managers.

    Managers would not guess, but would see directives like the number of bottles of the various brands they should have in stock. This transforms analytics into making decisions and minimizes the use of a manual judgment.

    The model may be re-trained on a weekly or monthly basis basing on the rate of change of the demand patterns.
6. Optional: What would break at scale? What would you track in production?
    Some challenges can manifest themselves at scale. Thousands of products may add to the time of training. New items can be affected by cold-start problems. Forecast accuracy may be reduced in situations where there is spike demand due to events. The demand patterns can change over time and as such, they need retraining.

    Monitoring of forecast error, stockout rate, holding cost, inventory turnover and general levels of service should be carried out in production. Monitoring of these measures is essential to ensure the system remains a source of business value and to enable one to identify problems in time.