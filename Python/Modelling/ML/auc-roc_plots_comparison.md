# AUC-ROC Plots

```Python
y_train_probs = bag_gb_.predict_proba(X_train)[:,1]
false_pos_rate1, true_pos_rate1, _ = roc_curve(y_train, y_train_probs)
roc_auc1 = auc(false_pos_rate1, true_pos_rate1)

y_train_probs2 = bag_dt_.predict_proba(X_train)[:,1]
false_pos_rate2, true_pos_rate2, _ = roc_curve(y_train, y_train_probs2)
roc_auc2 = auc(false_pos_rate2, true_pos_rate2)

y_train_probs3 = bag_rf_.predict_proba(X_train)[:,1]
false_pos_rate3, true_pos_rate3, _ = roc_curve(y_train, y_train_probs3)
roc_auc3 = auc(false_pos_rate3, true_pos_rate3)

y_train_probs4 = bag_knn_.predict_proba(X_train)[:,1]
false_pos_rate4, true_pos_rate4, _ = roc_curve(y_train, y_train_probs4)
roc_auc4 = auc(false_pos_rate4, true_pos_rate4)

y_train_probs5 = bag_mlp_.predict_proba(X_train)[:,1]
false_pos_rate5, true_pos_rate5, _ = roc_curve(y_train, y_train_probs5)
roc_auc5 = auc(false_pos_rate5, true_pos_rate5)

y_train_probs6 = bag_svc_.predict_proba(X_train)[:,1]
false_pos_rate6, true_pos_rate6, _ = roc_curve(y_train, y_train_probs6)
roc_auc6 = auc(false_pos_rate6, true_pos_rate6)

y_train_probs7 = bag_svc_.predict_proba(X_train)[:,1]
false_pos_rate7, true_pos_rate7, _ = roc_curve(y_train, y_train_probs7)
roc_auc7 = auc(false_pos_rate7, true_pos_rate7)

fig, (ax1,ax2) = plt.subplots(1, 2, figsize=(20,10))
ax1.plot(false_pos_rate1, true_pos_rate1, label='Gradient Boosting (area = %0.3f)' % roc_auc1, color='b')
ax1.plot(false_pos_rate2, true_pos_rate2, label='Decision Tree (area = %0.3f)' % roc_auc2, color='r')
ax1.plot(false_pos_rate3, true_pos_rate3, label='Random Forest (area = %0.3f)' % roc_auc3, color='g')
ax1.plot(false_pos_rate4, true_pos_rate4, label='KNN (area = %0.3f)' % roc_auc4, color='y')
ax1.plot(false_pos_rate5, true_pos_rate5, label='MLP (area = %0.3f)' % roc_auc5, color='pink')
ax1.plot(false_pos_rate6, true_pos_rate6, label='SVC (area = %0.3f)' % roc_auc6, color='orange')
ax1.plot(false_pos_rate7, true_pos_rate7, label='Logisitc Regression (area = %0.3f)' % roc_auc6, color='purple')
ax1.set_title('Training Data')

y_val_probs = prob_gb_bag
false_pos_rate1, true_pos_rate1, _ = roc_curve(y_val, y_val_probs)
roc_auc1 = auc(false_pos_rate1, true_pos_rate1)

y_val_probs2 = prob_dt_bag
false_pos_rate2, true_pos_rate2, _ = roc_curve(y_val, y_val_probs2)
roc_auc2 = auc(false_pos_rate2, true_pos_rate2)

y_val_probs3 = prob_rf_bag
false_pos_rate3, true_pos_rate3, _ = roc_curve(y_val, y_val_probs3)
roc_auc3 = auc(false_pos_rate3, true_pos_rate3)

y_val_probs4 = prob_knn_bag
false_pos_rate4, true_pos_rate4, _ = roc_curve(y_val, y_val_probs4)
roc_auc4 = auc(false_pos_rate4, true_pos_rate4)

y_val_probs5 = prob_mlp_bag
false_pos_rate5, true_pos_rate5, _ = roc_curve(y_val, y_val_probs5)
roc_auc5 = auc(false_pos_rate5, true_pos_rate5)

y_val_probs6 = prob_svc_bag
false_pos_rate6, true_pos_rate6, _ = roc_curve(y_val, y_val_probs6)
roc_auc6 = auc(false_pos_rate6, true_pos_rate6)

y_val_probs7 = prob_lr_bag
false_pos_rate7, true_pos_rate7, _ = roc_curve(y_val, y_val_probs7)
roc_auc7 = auc(false_pos_rate7, true_pos_rate7)

ax2.plot(false_pos_rate1, true_pos_rate1, label='Gradient Boosting (area = %0.3f)' % roc_auc1, color='b')
ax2.plot(false_pos_rate2, true_pos_rate2, label='Decision Tree (area = %0.3f)' % roc_auc2, color='r')
ax2.plot(false_pos_rate3, true_pos_rate3, label='Random Forest (area = %0.3f)' % roc_auc3, color='g')
ax2.plot(false_pos_rate4, true_pos_rate4, label='KNN (area = %0.3f)' % roc_auc4, color='y')
ax2.plot(false_pos_rate5, true_pos_rate5, label='MLP (area = %0.3f)' % roc_auc5, color='pink')
ax2.plot(false_pos_rate6, true_pos_rate6, label='SVC (area = %0.3f)' % roc_auc6, color='orange')
ax2.plot(false_pos_rate7, true_pos_rate7, label='Logisitc Regression (area = %0.3f)' % roc_auc7, color='purple')
ax2.set_title('Validation Data')

for ax in fig.axes:
    ax.plot([0, 1], [0, 1], 'k--')
    ax.set_xlim([-0.05, 1.0])
    ax.set_ylim([0.0, 1.05])
    ax.set_xlabel('False Positive Rate')
    ax.set_ylabel('True Positive Rate')
    ax.legend(loc="lower right")
    ```