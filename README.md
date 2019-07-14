# PPG Heart Beat for Cognitive Fatigue Prediction
Raw PPG waves & annotations from subjects playing computer games for 22 hours

## Goal 🏆

Predict "too tired to work" events from PPG data continuously monitored throughout their shift

## Predicting & preventing fatigue-related accidents 😴

Workers' cognitive fatigue is the cause of 2/3 of accidents in the mining industry and there are similar dangers in road and air transportation and any shift-work environments where people are working 12-hour shifts (eg hospitals).

The gold-standard for neuroscientists studying fatigue is an [electroencephalogram (EEG)](https://en.wikipedia.org/wiki/Electroencephalography) but it is hard to get good EEG measurements outside of a clinical setting. There has recently been more research using [electrocardiogram (ECG or EKG)](https://en.wikipedia.org/wiki/Electrocardiography) measurements, particularly using Heart Rate Variability (HRV) as a factor. Good ECG measurements are also not practical on people who are moving around in their working environment.

[Photoplethysmograph (PPG)](https://en.wikipedia.org/wiki/Photoplethysmogram) measurement on the ear is another technique to measure HRV and this can be packaged in a way that is accurate, comfortable and unobtrusive for people to wear all the way through their shift and on their drive home afterwards.

## 5-Gamer trial data 🎮

There were 5 participants, each attempting a 22 hour "shift" of computer gaming. For each participant there is:

- A PPG time-series (level of 660nm red light transmitted through participant's ear-lobe) sampled at approx 100Hz
- A diary of annotations including:
  - ['sleep-2-peak' reaction time](https://sleep-2-peak.com/) each hour
  - caffeine and food ingress and egress
  - self-assessment [Stanford sleepiness scale (1-7)](https://web.stanford.edu/~dement/sss.html) each hour

## Analysis 📈

Factors to derive could include:

  - every heartbeat (traditionally ECG "R-peak" but fastest-changing edge of the PPG curve may be a more accurate proxy)
  - heart rate (HR) and heart rate variability (HRV)
  - respiratory rate (RR)

All in order to estimate:

- Time to "too tired to work" epoch. This is the point at which you will lose the battle against falling asleep.

Consider:

- It's a "mean time to failure" problem
- **"Cognitive fatigue" is *not* the same as the sleepiness you feel every day at bedtime**
- Cleaning and annotating the data
- Dealing with gaps in the data (eg earpiece taken off)
- Dealing with noise in the data
- Factors to control or monitor better with subjects during future trials
- Possible sources of more 3rd-party fatigue data, for example [Sleep Centres](https://en.wikipedia.org/wiki/Polysomnography)


### Possible approach

For each gamer:

1. Clean the PPG .CSV data files -&gt; new raw PPG time-series file(s) (A)
2. Clean/normalise the annotations in the .CSV fatigue diary? -&gt; new annotations file (B)
3. Heartbeat peak detection to obtain nanosecond timestamps for every heartbeat in the PPG data (A) -&gt; new heartbeat timestamps file (C)
4. Calculate heart rate and heart rate variability from the heartbeat timestamps (C) -&gt; new time-series file (D)
5. Explore trends and anomalies in the HR & HRV data (D). -&gt; append new annotations to gamer’s annotation file (B)
6. Document all we learn about baselines, trends, anomalies and correlations with the annotations and any ideas for further factors that move us towards a mean-time-to-failure prediction of their “too tired to work” epoch.
7. -&gt; new time-series file of experimental attempts of time-to-“too tired to work”-epoch (F) 

8. Breath (respiration) detection to obtain nanosecond timestamps for every breath from the PPG data (A) and/or the heartbeat timestamps (C) -&gt; new breath timestamps file (E)
9. Calculate respiration rate from (E) -&gt; append Respiratory Rate column to (D)
10. Revisit 5-7 with extra respiration factor

11. Eyes closed and/or “nodding dog” detection from .WMV webcam videos -&gt; append new micro-sleep annotations to gamer’s annotation file (B)
12. Revisit 5-7 for correlations in (D) with the new micro-sleep annotations

### For new annotations

Don’t worry if 7 is rubbish at the moment because there are too few events to make any sense of. Still try!

For new anomalies you find in 5, I can review webcam video of the gamer at these timestamps to see what they are indications of and then add appropriate "ground truth" annotations to (B) with accurate timestamps. Just contact me through Kaggle to do this. Also if anyone knows how to *automatically* detect "eyes closed" and/or “nodding dog” micro-sleep events from .WMV webcam videos please let me know.

## Bibliography  📚

A great place to start is this flawed but nevertheless interesting 2013 article from Korea: 

- [Gang Li & Wan-Young Chung: Detection of Driver Drowsiness Using Wavelet Analysis of Heart Rate Variability and a Support Vector Machine Classifier](https://www.researchgate.net/publication/259246802_Detection_of_Driver_Drowsiness_Using_Wavelet_Analysis_of_Heart_Rate_Variability_and_a_Support_Vector_Machine_Classifier)

which of course refers to this seminal 1996 article on LF/HF HRV analysis:

- [Task Force of the European Society of Cardiology and the North American Society of Pacing and Electrophysiology: Heart rate variability: Standards of measurement, physiological interpretation and clinical use](https://www.researchgate.net/publication/303183789_Heart_rate_variability_Standards_of_measurement_physiological_interpretation_and_clinical_use_Task_Force_of_the_European_Society_of_Cardiology_and_the_North_American_Society_of_Pacing_and_Electrophysi)

## Acknowledgements 🙏

Thanks to the 5 anonymous gamers who donated a day of their life for this and to the young electronic engineers who donated months of their life building the prototypes that collected this PPG dataset. We wouldn't be here without you all.

[This dataset](https://www.researchgate.net/publication/330842559_5_Gamers_x_24_hours) is part of the [Predicting Cognitive Fatigue with Photoplethysmography (PPG)](https://www.researchgate.net/project/Predicting-Cognitive-Fatigue-with-Photoplethysmography-PPG) project.