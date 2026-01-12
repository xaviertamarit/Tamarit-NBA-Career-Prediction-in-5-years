# NBA Rookie Career Longevity Predictor 🏀

## 📌 Project Overview
This project aims to predict the career longevity of NBA rookies using machine learning. The primary goal is to determine if a player will remain in the league for **5 years or more** based on their first-year statistical performance.

This is a binary classification problem characterized by a highly imbalanced dataset (approximately 85% of rookies reach the 5-year mark), which required specialized data processing and model evaluation techniques.


## 📖 Data Dictionary
The dataset consists of the following performance metrics collected during a player's rookie season:

* **Id**: Player Identifier
* **GP**: Games Played
* **MIN**: Minutes Played
* **PTS**: Points Per Game
* **FGM**: Field Goals Made
* **FGA**: Field Goals Attempts
* **FG%**: Field Goals Percent
* **3P Made**: 3-Points Made
* **3PA**: 3-Points Attempts
* **3P%**: 3-Points Percent
* **FTM**: Free Throw Made
* **FTA**: Free Throw Attempts
* **FT%**: Free Throw Percent
* **OREB**: Offensive Rebounds
* **DREB**: Defensive Rebounds
* **REB**: Rebounds
* **AST**: Assists
* **STL**: Steals
* **BLK**: Blocks
* **TOV**: Turnovers
* **TARGET_5Yrs**: Outcome Label (1 if career length >= 5 years, 0 otherwise)

## 🎯 Objectives
* **Performance Prediction**: Build a robust classifier to identify future NBA veterans versus those who will exit the league early.
* **Risk Mitigation**: Prioritize the identification of "busts" (Class 0) to help teams avoid high-risk investments.
* **Comparative Analysis**: Evaluate the effectiveness of different balancing techniques, including Cost-Sensitive Learning (Balanced Weights) and SMOTE.

## 📊 Dataset & Cleaning
The raw data was subjected to a rigorous cleaning process to ensure model reliability:
* **Data Quality**: Reduced the dataset from ~8,000 to **4,802 observations** by removing impossible values (e.g., shooting percentages > 100%) and statistical outliers that exceeded historical NBA records.
* **Integrity**: The final dataset contains **zero missing values (NaNs)**.
* **Preprocessing**: Applied **MinMaxScaler** to normalize features, which is critical for distance-based models like SVM and Perceptron.

## 🧪 Modeling Strategy
We explored a wide range of algorithms to address the class imbalance:
1.  **Baseline Models**: Logistic Regression, Decision Trees, and Perceptrons.
2.  **Ensemble Methods**: Random Forest and AdaBoost.
3.  **Balanced Approaches**: SVM with RBF Kernel and `class_weight='balanced'`.
4.  **Oversampling**: Implementing **SMOTE** to generate synthetic minority samples.

## 🏆 Final Results



## 🛠️ Requirements
To run this project, you need the following Python libraries:
* `scikit-learn`
* `pandas`
* `numpy`
* `matplotlib`
* `seaborn`
* `imbalanced-learn`

## 📚 References & Resources

### Data Sources
* **Kaggle Competition**: [NBA Career Prediction](https://www.kaggle.com/competitions/uts-advdsi-22-02-nba-career-prediction/data) - Primary source for the training and testing datasets used in this project.
* **Basketball Reference**: [https://www.basketball-reference.com/](https://www.basketball-reference.com/) - External resource used for cross-referencing historical records and validating/cleaning erroneous data points.

### Academic Research
* **SMOTE**: Chawla, N. V., Bowyer, K. W., Hall, L. O., & Kegelmeyer, W. P. (2002). *SMOTE: Synthetic Minority Over-sampling Technique*. Journal of Artificial Intelligence Research, 16, 321–357.

### Technical Documentation
* **Scikit-learn User Guide**: [Imbalanced Datasets](https://scikit-learn.org/stable/modules/imbalanced_learn.html) - Documentation on handling class imbalance in classification tasks.
* **Scikit-learn API**: [Gaussian Naive Bayes](https://scikit-learn.org/stable/modules/generated/sklearn.naive_bayes.GaussianNB.html) - Technical details for our selected final model.

