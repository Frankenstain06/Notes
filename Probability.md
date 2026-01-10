# Probability

1. If you have 3 coins and you flip them all at once, what is the probability of getting exactly 3 heads?

   - A) 1/8
   - B) 3/8
   - C) 1/2
   - D) 5/8

   **Answer:** A) 1/8
    **Explanation:** We have 3 coins (3 will be the power of 2). The 2 comes from the two possible outcomes of each coin (head or tail). So, the total number of outcomes is 2^3 = 8. The favorable outcomes for getting exactly 3 heads is only 1 (HHH). Therefore, the probability is 1/8.

    **Formula:** Probability = (Number of favorable outcomes) / (Total number of outcomes)

**Disjoint :** Disjoint events, also known as mutually exclusive events, are events that cannot occur at the same time. For example, when flipping a coin, getting heads and tails are disjoint events because you cannot get both outcomes in a single flip.

   **Formula:**  \( P(A \cup B) = P(A) + P(B) \)

**Joint :** Joint events, on the other hand, are events that can occur at the same time. For example, when rolling a pair of dice, getting a sum of 7 and getting an even number on one of the dice are joint events because both can happen simultaneously.

   **Formula:**  \( P(A \cup B) = P(A) + P(B) - P(A \cap B) \)

**Independent :** Independent events are events where the occurrence of one event does not affect the occurrence of another event. For example, flipping a coin and rolling a die are independent events because the outcome of the coin flip does not influence the outcome of the die roll.

   **Formula:** \( P(A \cap B) = P(A) \times P(B) \)  

**Complementary :** If there are 10 boys and 6 of them wearing hats then the probability of selecting a boy wearing a hat is 6/10 or 3/5. The probability of selecting a boy not wearing a hat is 4/10 or 2/5. The sum of these probabilities is 1.

   **Formula:** \( P(A) + P(\text{not } A) = 1 \) or \( P(\text{not } A) = 1 - P(A) \)

**Conditional :** Conditional probability is the probability of an event occurring given that another event has already occurred. For example, if you have a deck of cards and you want to find the probability of drawing an ace given that you have already drawn a king, you would use conditional probability. There is a connection between independent and conditional probabilities. Conditional is dependent.

   **Formula:** \( P(A|B) = \frac{P(A \cap B)}{P(B)} \)
   **Formula:** \( P(A \cap B) = P(A|B) \times P(B) \)

**Bayes' Theorem :** Bayes' Theorem is a way to find a conditional probability when the reverse conditional probability is known. It relates the conditional and marginal probabilities of random events.

   **Formula:** \( P(A|B) = \frac{P(B|A) \times P(A)}{P(B)} \)