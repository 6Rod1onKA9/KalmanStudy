# Kalman Filter Study

**Purpose of the Work:**
Understand the operation of the Kalman filter and its application principles. Study the impact of various filter parameters on the results of signal smoothing. Learn how to analyze filtering results, considering noise variance values before and after filtering.

# Theoretical Information

*Definition*

The **Kalman Filter** is a mathematical filtering method used to remove noise from data and improve measurement accuracy. In the context of coordinate systems, the Kalman filter is applied for two main purposes:

1) Filtering of physical signal measurements: If we have a series of measurements (e.g., from sensors) that contain a lot of noise, the Kalman filter helps to "clean" this data, resulting in a more accurate coordinate value.

2) Refining already determined coordinates: After determining coordinates based on several measurements (e.g., using trilateration or multilateration), the Kalman filter refines these coordinates, compensating for errors that occurred during measurements.

- **The Kalman filter is based on two stages:**

1) Prediction: At this stage, the filter makes a prediction based on the previous state (coordinate) and the object's motion model. For example, if we know that a car is moving at 50 km/h, we can predict where it will be in 1 minute.
2) Update based on new data: When the filter receives a new measurement (e.g., GPS coordinates), it updates its estimate, taking into account the new data and comparing it with the predicted state. If the new measurement significantly differs from the predicted value, the filter only partially "trusts" the new measurement, considering potential errors.

# Tasks

1) **Code Initialization:**

- Use the code provided in the "Theoretical Information" section as a base template.
- Ensure that all Kalman filter parameters (F, H, Q, R, P, x) are set correctly and match the initial variant.

**Parameter Impact Analysis**

*Sequentially change the values of each of the following Kalman filter parameters:*

- **Process Noise Covariance Matrix** (Q): Increase and decrease the values, and analyze how this impacts the prediction.
- **Measurement Noise Covariance Matrix** (R): Modify this parameter to see how the filter responds to changes in measurement reliability.
- **Initial Covariance Matrix** (P): Experiment with different initial uncertainties regarding the state.
- **Initial State Estimate**: Try various initial values and observe how this affects the convergence of the filter.
- **Constant Signal Component** (offset): Change the signal offset to evaluate how the filter adapts to a shifted signal.
- **Total Modeling Time** (total_time): For configurations with highly inertial parameters, change the total simulation time to ensure the filter has enough time to "tune" and stabilize its results.

**Comparison of Results**

*For each parameter combination:*

- Calculate noise variance before filtering and after filtering.
- Create a graph that shows the filtering results compared to the true signal and the noisy signal.
- Take screenshots of each graph and include them in the report.

**Analysis and Conclusions**

- Record the noise variance values before and after filtering.
- Comment on the results for each filtering case.
- Explain how the change in a specific parameter affected the prediction, state correction, and variance change.
- Formulate general conclusions about the behavior of the Kalman filter under different parameter combinations.

# Solution

**1) Parameter configuration**

- **Process Noise Covariance Matrix** (Q): 1
- **Measurement Noise Covariance Matrix** (R): 10
- **Initial Covariance Matrix** (P): 1
- **Initial State Estimate**: 0
- **Constant Signal Component** (offset): 10
- **Total Modeling Time** (total_time): 1

![image](https://github.com/user-attachments/assets/cf058b85-123f-4ddf-a977-f2b16e814c6a)
![image](https://github.com/user-attachments/assets/a96e0381-233c-4469-98cf-cad079072cf5)

 - **Result-conclusion:**
The graph illustrates that the Kalman filter estimate closely tracks the true signal while effectively minimizing noise compared to the noisy signal. Although the filter smooths the values, it responds gradually to changes in the signal due to the high measurement noise level. **In this scenario**, the filter operates effectively with a process variance of 𝑄 = 1 and a measurement variance of 𝑅 = 10. Reducing 𝑅 makes the filter more responsive to fluctuations but also increases the noise in the estimate. Conversely, raising 𝑄 enables quicker adaptation to changes but results in a noisier estimate.

**2) Parameter configuration**

- **Process Noise Covariance Matrix** (Q): 0.3
- **Measurement Noise Covariance Matrix** (R): 3
- **Initial Covariance Matrix** (P): 0.7
- **Initial State Estimate**: 10
- **Constant Signal Component** (offset): 2
- **Total Modeling Time** (total_time): 0.4

![image](https://github.com/user-attachments/assets/3eb7dbbb-b400-4c61-976a-6f67ec756809)
![image](https://github.com/user-attachments/assets/1048f9d0-3c1f-48f1-8880-2d88a8b47e16)

 - **Result-conclusion:**
The Kalman filter effectively reduced the noise variance in the processed signal, demonstrating its ability to smooth the data and achieve a much lower noise level. With 𝑄 = 0.3 and 𝑅 = 3, the Kalman filter effectively reduces the noise level, though it may slightly suppress rapid fluctuations in the signal due to the low process variance. The 𝑅 parameter controls the filter's sensitivity to measurements—a lower 𝑅 increases sensitivity but also introduces more noise. On the other hand, raising 𝑄 allows the filter to adapt more quickly to changes in the signal but at the cost of adding more noise to the smoothed output. The current settings achieve a good balance for smoothing, though adjustments to 𝑅 and 𝑄 can optimize the trade-off between sensitivity and stability

**3) Parameter configuration**

- **Process Noise Covariance Matrix** (Q): 10
- **Measurement Noise Covariance Matrix** (R): 30
- **Initial Covariance Matrix** (P): 15
- **Initial State Estimate**: -10
- **Constant Signal Component** (offset): 8
- **Total Modeling Time** (total_time): 20

![image](https://github.com/user-attachments/assets/4b4201aa-9724-47f7-baa1-89992d8152dd)
![image](https://github.com/user-attachments/assets/d69e95b2-96d9-49c6-8561-931d63242cd1)

- **Result-conclusion:**
The results indicate a substantial reduction in variance after filtering, highlighting the Kalman filter's effectiveness in noise reduction. However, with 𝑅 = 30, the filter becomes less responsive to changes in the measurements. In this example, using a filter with 𝑄 = 10 and 𝑅 = 30 achieves effective noise reduction while preserving the stability of the filtered signal. Reducing 𝑅 would enhance the filter's responsiveness to sudden changes in measurements but might introduce more noise. Increasing 𝑄 would enable quicker adaptation to abrupt changes but at the expense of greater fluctuations in the filtered output. These parameters strike a good balance between smoothing and accuracy, though adjusting 𝑄 and 𝑅could yield better results under different conditions.
