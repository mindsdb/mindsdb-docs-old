---
id: predictive-maintenance
title: Predictive Maintenance
---

| Industry       | Department | Role               |
|----------------|------------|--------------------|
| High-Tech & Manufacturing | Operations | Data Scientist |

## Processed Dataset 

###### [![Data](https://img.shields.io/badge/GET--DATA-RoboticFailure-green)](https://github.com/mindsdb/mindsdb-examples/tree/master/others/robotic_failure/dataset)


```python
import mindsdb
import pandas as pd
from sklearn.metrics import r2_score


def run():
    mdb = mindsdb.Predictor(name='robotic_failure')

    mdb.learn(from_data='dataset/train.csv', to_predict=['target'])

    predictions = mdb.predict(when='test.csv')

    pred_val = [x['target'] for x in predictions]
    real_val = list(pd.read_csv('dataset/test.csv')['target'])

    accuracy = r2_score(real_val, pred_val)
    print(f'Got an r2 score of: {accuracy}')

    #show additional info for each transaction row
    additional_info = [x.explanation for x in predictions]

    return {
        'accuracy': accuracy,
         'accuracy_function': 'balanced_accuracy_score',
         'backend': backend,
         'additional_info': additional_info
    }


# Run as main
if __name__ == '__main__':
    print(run())
```

{'accuracy': 0.8399922571492469, 'accuracy_function': 'balanced_accuracy_score', 'backend': 'lightwood'}
