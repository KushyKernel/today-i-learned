# Evaluating features of ML algorithms

```Python
from sklearn.model_selection import cross_val_score, RepeatedStratifiedKFold

def get_models():
    models = dict()
    for i in range(10, 31):
        models[str(i)] = BaggingClassifier(base_estimator=LogisticRegression(max_iter = 1000, random_state=123),
        n_estimators=100, max_samples=0.025, max_features=i)
    return models


def evaluate_model(model, X_, y_):
    cv = RepeatedStratifiedKFold(n_splits=5, n_repeats=3, random_state=123)
    scores = cross_val_score(model, X_, y_, scoring='f1_macro', cv=cv, n_jobs=-1, error_score='raise')
    return scores

models = get_models()

results, names = list(), list()
for name, model in models.items():
    scores = evaluate_model(model, X_, y_)
    results.append(scores)
    names.append(name)
    print(">%s %.3f  (%.3f)"  % (name, np.mean(scores), np.std(scores)))
    
plt.boxplot(results, labels=names, showmeans=True)
plt.show
```