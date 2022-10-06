# mobile-Anomaly-Detection
Project for Mobile Robotic course at the University of Verona - A.Y. 2021/2022

## Purpose

Nowadays in a robotic system hot topics are process monitoring, anomaly detection and maintanence. In fact, it is extremely difficult to detect in advance anomalous behaviours in order to preserve the high quality standard of the system. 
The main idea for adressing that issue is to build a real-time anomaly detection model, from collected time series data, which is able to identify any fault data that do not conform to historical patterns.
This project is an overview of different baselines for detecting anomalies applied on different datasets.

## Dataset 
The methods has been tested on two different datasets: 
- **Pepper, swat and boat** datasets which you can load by Dataset class
- **Kairos** which has been acquired in the ICELab at the University of Verona. In this case the original dataset is processed choosing less number of sensors. In particular, there are two different folders: "Campioni_iniziali" and "Campione_finale". Each of them is composed of different submodels based on what kind of sensors we keep.

## Methods 
### PCA
The aim of Principal Component Analysis(PCA) is to reduced a process in a subspace of maximum variance. Exploiting this tool we can compute a space sufficient for preserving relevant information. Going back to the original data we can find an error of reconstruction which it is higher if the starting data are affected by anomalies. At training time we build a model analyzing only the error of nominal data. At testing time, an anomalous behaviours is detected if the signal is not within the model. Some acceptability criteria are defined for detecting the anomaly, in particular we have median, score, quantile and gaussian.
- **Median**: we raise an alert whenever the errors( also called L2 norm of the residuals) at testing time exceeds the median of the same values computed at training time multiplied by a constant safety factor. In this case all features are considered together at each time frame, since all the signals collapse to a single value called anomaly score.
- **Score**: it is the same idea of Median, but the threshold in this case is computed with a different criteria.
- **Quantile**: we again analyse the errors at testing time. At training time we compute the upper and lower bound as the 5% and 95% quantiles of the distribution on the nominal data. In this case we raise when the error overcames the bounds.
- **Gaussian**: at training time we fit the with a mixture of multimodal gaussian distributions the data. At testing time, we compute the Mahalanobis distance from the current data and each component of the gaussian mixture model; finally, we keep the minimum distance as the anomaly score and we compare it with a fixed threshold set in advance. In this way we analyse whether the measurement matrix can fit at least one of the gaussian models within the mixture.

Inspired by:
> Fiorini et al., IndRAD: A Benchmark for Anomaly Detection on Industrial Robots, ICPR workshops 2022.

## Results 

## Usage
In order to make the project more interactive, all the project is developed in a ```colab``` file, which is composed of different sections.

You need to run all the first sections. Then, you can decide which dataset and method to use. Instead for testing the section is only one.
