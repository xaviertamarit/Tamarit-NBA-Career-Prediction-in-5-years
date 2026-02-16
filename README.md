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
* **Comparative Analysis**: Evaluate the effectiveness of different balancing techniques, including Cost-Sensitive Learning (Balanced Weights), SMOTE , Ensemble methods and Neural Networks.

## 📊 Dataset & Cleaning
The raw data was subjected to a rigorous cleaning process to ensure model reliability:
* **Data Quality**: Reduced the dataset from ~8,000 to **4,802 observations** by removing impossible values (e.g., shooting percentages > 100%) and statistical outliers that exceeded historical NBA records.
* **Integrity**: The final dataset contains **zero missing values (NaNs)**.
* **Preprocessing**: Applied **MinMaxScaler** to normalize features, which is critical for distance-based models like SVM and Perceptron.

## 🧪 Modeling Strategy
We explored a wide range of algorithms to address the class imbalance:
1.  **Baseline Models**: Logistic Regression, Decision Trees, and Perceptrons.
2.  **Ensemble Methods**: Random Forest, AdaBoost, Soft Voting, and Stacking.
3.  **Balanced Approaches**: SVM with RBF Kernel and `class_weight='balanced'`.
4.  **Advanced Neural Networks**: Multi-Layer Perceptron (MLP) using a "funnel" architecture (16, 8) and ReLU activation.
5.  **Oversampling**: Implementing **SMOTE** (Synthetic Minority Over-sampling Technique) to generate synthetic minority samples.
6.  **Feature Selection**: Transitioning from a full-statistical set to a targeted "Top-5" selection (GP, MIN, PTS, FG%, REB) to reduce noise.

## 📊 Performance Comparison
Through iterative testing, we identified a clear "Rookie Information Ceiling" at an F1-Macro score of approximately 0.56. The hierarchy of models revealed different strategic utilities:

| Model Strategy | F1-Macro | TP | TN | FP | FN | Strategic Utility |
| :--- | :---: | :---: | :---: | :---: | :---: | :--- |
| GNB (Top-5 Features) | **0.5660** | 1,064 | 57 | 164 | 156 | **Best for Talent Discovery** |
| GNB (Full Features) | 0.5564 | 886 | 104 | 334 | 117 | Balanced Scouting |
| SVM (Balanced) | 0.5367 | 751 | 141 | 459 | 80 | **Best for Risk Mitigation** |


## 🏆 Final Results & Key Findings
* **Highest f1-score**: The **Optimized Gaussian Naive Bayes (GNB)** with 5 features and `var_smoothing=0.001` emerged as the best model. It achieved the project's highest **F1-Macro of 0.5660**.
* **Simplicity vs. Complexity**: Simple probabilistic models (GNB) with targeted feature engineering outperformed complex deep learning (MLP) and ensemble (Stacking) architectures.
* **The "Talent Tax"**: Models that prioritize finding "busts" (like SVM) incur a high cost of opportunity, often misclassifying successful players as failures. 
* **The Year-1 Signal**: The results prove that while rookie stats are strong indicators, the "signal" for a 5-year career is not fully formed in the first season. Longevity is heavily influenced by variables not present in box scores, such as injuries and work ethic.

## 📈 Strategic Conclusion
There is no "one fits all" model. 
1. **Aggressive Teams**: Should use the **GNB Top-5** to find stars while accepting the risk of "busts".
2. **Conservative Contenders**: Should use the **SVM** to avoid wasting roster spots on high-risk players.
3. **Teams in Transition **: Should use the **Full-Feature GNB**. This model serves as a "balanced bridge," considering the complete statistical profile of the rookie. It is perfect for franchises with a healthy salary cap that want to find "diamonds in the rough" without the extreme bias of the Top-5 approach.

## 🛠️ Requirements
To run this project, you need the following Python libraries:
* `numpy`
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
* **Stacked Generalization (Stacking)**: Wolpert, D. H. (1992). *Stacked Generalization*. Neural Networks, 5(2), 241-259. - The seminal paper that introduced the two-layer meta-learning architecture used in this project.
* **Voting Classifiers**: Kuncheva, L. I. (2004). *Combining Pattern Classifiers: Methods and Algorithms*. Wiley. - A foundational text on how combining independent models through voting (Soft/Hard) reduces variance and improves robustness.
* **Scikit-learn Documentation**: [Ensemble Methods User Guide](https://scikit-learn.org/stable/modules/ensemble.html) - Official documentation covering the implementation of `VotingClassifier` and `StackingClassifier`.

### Technical Documentation
* **Scikit-learn User Guide**: [Imbalanced Datasets](https://scikit-learn.org/stable/modules/imbalanced_learn.html) - Documentation on handling class imbalance in classification tasks.
* **Scikit-learn API**: [Gaussian Naive Bayes](https://scikit-learn.org/stable/modules/generated/sklearn.naive_bayes.GaussianNB.html) - Technical details for our selected final model.

