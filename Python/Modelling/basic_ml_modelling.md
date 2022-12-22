# Applying Basic Machine Learning Quickly

A multitude of machine learning algorithms can be applied using this code.

Importing `metrics` will help asses the models performance at base level for the chose dataset:

```Python
from sklearn.linear_model import LogisticRegression
from sklearn.neighbors import KNeighborsClassifier
from sklearn.tree import DecisionTreeClassifier
from sklearn.ensemble import RandomForestClassifier, GradientBoostingClassifier
from sklearn.neural_network import MLPClassifier
from sklearn.svm import SVC

from sklearn.metrics import accuracy_score, f1_score, precision_score, recall_score, roc_auc_score 

models={
    "Logistic Regression": LogisticRegression(),
    "KNeighbors": KNeighborsClassifier(),
    "Decision Tree": DecisionTreeClassifier(),
    "Random Forest": RandomForestClassifier(),
    "Gradient Boosting": GradientBoostingClassifier(),
    "MLP Classifier": MLPClassifier(),
    "Support Vector Classifier": SVC()  
}

for i in range(len(list(models))):
    model = list(models.values())[i]
    model.fit(X_train, y_train)  #Train Models
    
    #Make Predictions
    y_train_pred = model.predict(X_train)
    y_val_pred = model.predict(X_val)
    
    #Training set performance
    train_acc = accuracy_score(y_train, y_train_pred)
    train_f1 = f1_score(y_train, y_train_pred, average='weighted')
    train_precision = precision_score(y_train, y_train_pred)
    train_recall = recall_score(y_train, y_train_pred)
    train_rocauc = roc_auc_score(y_train, y_train_pred)
    
    #Validation set performance
    val_acc = accuracy_score(y_val, y_val_pred)
    val_f1 = f1_score(y_val, y_val_pred, average='weighted')
    val_precision = precision_score(y_val, y_val_pred)
    val_recall = recall_score(y_val, y_val_pred)
    val_rocauc = roc_auc_score(y_val, y_val_pred)
    
    print(list(models.keys())[i])
    
    print("Model performance for Training set")
    print("- Accuracy: {:.4f}".format(train_acc))
    print("- F1 Score: {:.4f}".format(train_f1))
    print("- Precision: {:.4f}".format(train_precision))
    print("- Recall: {:.4f}".format(train_recall))
    print("- ROC AUC Score: {:.4f}".format(train_rocauc))
    
    print('--------------------------------------')
    
    print("Model performance for Validation set")
    print("- Accuracy: {:.4f}".format(val_acc))
    print("- F1 Score: {:.4f}".format(val_f1))
    print("- Precision: {:.4f}".format(val_precision))
    print("- Recall: {:.4f}".format(val_recall))
    print("- ROC AUC Score: {:.4f}".format(val_rocauc))
    
    print('='*35)
    print('\n')
```
