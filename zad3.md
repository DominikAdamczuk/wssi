```
import numpy as np
from collections import Counter

class Node:
  def __init__(self, feature=None, threshold=None, left=None, right=None, *, value=None):
    self.feature = feature
    self.threshold = threshold
    self.left = left
    self.right = right
    self.value = value

  def is_leaf_node(self):
    return self.value is not None


class DecisionTree:
  def __init__(self, min_samples_split=2, max_depth=100, n_features=None):
    self.min_samples_split=min_samples_split
    self.max_depth=max_depth
    self.n_features=n_features
    self.root=None

  def fit(self, X, y):
    self.n_features = X.shape[1] if not self.n_features else min(self.n_features, X.shape[1])
    self.root = self._grow_tree(X, y)

  def _grow_tree(self, X, y, depth=0):
    pass

  def _best_split(self, X, y, feat_idxs):
    pass

  def _information_gain(self, y, X_column, threshold):
    parent_entropy = self._entropy(y)

    left_index, right_index = self._split(X_column, threshold)

    if len(left_index)==0 or len(right_index)==0:
      return 0

    amounts = len(y)
    left_amounts, right_amounts = len(left_index), len(right_index)

    left_entropy = self._entropy(y[left_index])
    right_entropy = self._entropy(y[right_index])

    child_entropy = (left_amounts/amounts)*left_entropy+(right_amounts/amounts)*right_entropy

    return parent_entropy-child_entropy

  def _split(self, X_column, split_thresh):
    left_index = np.argwhere(X_column <= split_thresh).flatten()
    right_index = np.argwhere(X_column > split_thresh).flatten()

    return left_index, right_index

  def _entropy(self, y):
    hist = np.bincount(y)
    ps = hist / len(y)
    return -np.sum([p*np.log(p) for p in ps if p>0])

  def _traverse_tree(self, x, node):
    if node.is_leaf_node():
      return node.value

    if x[node.feature] <= node.threshold:
      return self._traverse_tree(x, node.left)

    return self._traverse_tree(x, node.right)

  def predict(self, X):
    return np.array([self._traverse_tree(x, self.root) for x in X])



from sklearn import datasets
from sklearn.model_selection import train_test_split
"""from decision_tree import DecisionTree"""

data = datasets.load_iris()
X, y = data.data, data.target

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=1234)

clf = DecisionTree(max_depth=10)
clf.fit(X_train, y_train)
predictions = clf.predict(X_test)

def accuracy(y_test, y_pred):
  return np.sum(y_test == y_pred) / len(y_test)

acc = accuracy(y_test, predictions)
print(acc)
```
