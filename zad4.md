```
import numpy as np

class Neuron:
    def __init__(self, n_inputs, bias = 0., weights = None):
        self.b = bias
        if weights: self.ws = np.array(weights)
        else: self.ws = np.random.rand(n_inputs)

    def _f(self, x):
        return max(x*.1, x)

    def __call__(self, xs):
        return self._f(xs @ self.ws + self.b)

layer1hidden=[Neuron(3) for _ in range(4)]
layer2hidden=[Neuron(4) for _ in range(4)]
layer3out=[Neuron(4) for _ in range(1)]

def sigmoid(x):
    return 1 / (1+np.exp(-x))

def function(layers, x):
    for i, layer in enumerate(layers):
        if i == len(layers)-1:
            x = np.array([sigmoid(neuron(x)) for neuron in layer])
        else:
            x = np.array([neuron(x) for neuron in layer])
    return x

test = np.array([1.0, 2.5, -4.9])

layers = [layer1hidden, layer2hidden, layer3out]
out = function(layers, test)
print(out)
```


```
import networkx as nx
#import matplotlib.pyplot as plt

Graph = nx.DiGraph()

layers = [3,4,4,1]

for layer in range(len(layers)-1):
    for start_neuron in range(layers[layer]):
        for end_neuron in range(layers[layer+1]):
            Graph.add_edge(f"{layer}_{start_neuron}", f"{layer+1}_{end_neuron}")

position = {}
for layer, layers in enumerate(layers):
    for neuron in range(layers):
        position[f"{layer}_{neuron}"] = (layer, -neuron)

nx.draw(Graph, position, with_labels=False, node_size=2000, node_color="red")
#plt.show()
```
