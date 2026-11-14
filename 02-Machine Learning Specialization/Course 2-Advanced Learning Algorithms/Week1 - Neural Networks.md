# Neurons and the Brain

## Overview
Modern Neural Networks are inspired by biological brains. While the math we use today is a highly simplified version of actual biology, the core concept remains the same: taking inputs, processing them, and producing an output.

---

## 1. The History of Neural Networks

*   **1980s - early 1990s:** Neural networks were popular and used for simple tasks.
*   **Late 1990s:** They fell out of favor because computers were too slow and data was too scarce.
*   **2005 - Present:** A massive resurgence. They are now the foundation of modern AI (speech recognition, image recognition, and NLP/ChatGPT).
![](../../00-Attachments/Pasted%20image%2020261114235133.png)
---

## 2. Biological vs. Mathematical Neurons

*   **Biological Neuron:** Receives electrical signals through **dendrites** (inputs), processes them in the **cell body**, and passes the signal down the **axon** to the next neuron (output).
*   **Mathematical Neuron:** Takes numerical inputs (e.g., the number 2), performs a calculation, and outputs a single number (e.g., 0.7). 

The math model is incredibly simplified, but stringing millions of these mathematical neurons together allows us to solve complex problems.
![](../../00-Attachments/Pasted%20image%2020261114235139.png)
---

## 3. Why Now? (The Breakthrough)

Why did neural networks suddenly become so powerful after being ignored for a decade?
It comes down to two things:
1.  **Faster Hardware:** The invention and optimization of **GPUs** (Graphics Processing Units) allowed us to run massive neural networks in a reasonable amount of time.
2.  **Big Data:** The internet created massive datasets.

![](../../00-Attachments/Pasted%20image%2020261114235146.png)
### The Performance Graph
Look at the graph comparing "Traditional AI" to Neural Networks:
*   **Traditional AI (e.g., Linear Regression):** Performance plateaus after a certain amount of data. It stops getting better.
*   **Small/Medium Neural Networks:** Performance continues to rise with more data, but eventually plateaus.
*   **Large Neural Networks:** As long as you feed it massive amounts of data (**Big Data**) AND have fast enough computers (GPUs) to process it, the performance *keeps going up*. It scales beautifully.

> [!important] The Key Takeaway
> For traditional algorithms, throwing more data at the problem eventually stops helping. For large neural networks, **more data + more compute = better performance**. This is why deep learning has exploded in the last decade.

![](../../00-Attachments/Pasted%20image%2020261114235153.png)


# Demand Prediction (Neural Network Example)

## Overview
This note introduces the fundamental building blocks of a Neural Network using a real-world example: predicting whether a t-shirt will be a "top seller" based on various factors.
![](../../00-Attachments/Pasted%20image%2020261115000438.png)
---

## 1. The Single Neuron (Logistic Regression)

Before building a network, we start with a single neuron. 
Imagine we only have one input feature: `price`.

*   **Input (x):** Price of the shirt.
*   **Output (a):** Probability of being a top seller (between 0 and 1).
*   **Activation:** The output is calculated using the **Sigmoid function** (which is just Logistic Regression).
    `a = sigmoid(w * x + b)`

If the price is low, the probability of being a top seller is high (the curve is high on the left). If the price is high, the probability is low.
![](../../00-Attachments/Pasted%20image%2020261115000445.png)
![](../../00-Attachments/Pasted%20image%2020261115000507.png)
---

## 2. Building a Layer (Multiple Neurons)

In reality, "price" alone doesn't determine if a shirt sells well. We have multiple inputs:
`x = [price, shipping_cost, marketing, material]`

Instead of feeding all these directly into the final output, a neural network creates a **Hidden Layer**. The neurons in this layer try to learn intermediate concepts:
*   **Neuron 1:** Learns "Affordability" (based on price and shipping).
*   **Neuron 2:** Learns "Awareness" (based on marketing budget).
*   **Neuron 3:** Learns "Perceived Quality" (based on material and price).

> [!info] Terminology
> *   **Input Layer:** The raw data (`x`). (4 numbers)
> *   **Hidden Layer:** The intermediate calculations. (3 numbers, called **Activations**)
> *   **Output Layer:** The final prediction. (1 number)

The output layer takes the three activations from the hidden layer and combines them to make the final prediction: "Probability of being a top seller."
![](../../00-Attachments/Pasted%20image%2020261115000520.png)
---

## 3. Feature Engineering vs. Neural Networks

*   **Manual Feature Engineering:** In traditional ML, a human has to manually create features (e.g., `x3 = x1 * x2`).
*   **Neural Networks:** You don't have to manually engineer features! You just feed the raw inputs into the hidden layer, and the network *learns* the best intermediate features (like "affordability") on its own during training. 

---

## 4. Multiple Hidden Layers (Deep Learning)

A neural network can have many hidden layers. Each layer builds on the previous one to learn more complex patterns.

*   **1st Hidden Layer:** Learns simple features (e.g., edges, shapes, or basic affordability).
*   **2nd Hidden Layer:** Combines simple features into more complex ones.
*   **3rd Hidden Layer:** Combines those into even more complex concepts.

> [!note] Neural Network Architecture
> The way you choose to connect the neurons (how many layers, how many neurons per layer) is called the **Architecture**. A network with multiple hidden layers is called a **Multilayer Perceptron (MLP)** or a **Deep Neural Network**.

![](../../00-Attachments/Pasted%20image%2020261115000532.png)