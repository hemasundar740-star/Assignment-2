Assignment-2 README content
# Agentic AI Assignment-02

## Descriptive Questions

### 1. What happens when we give a sentence to an LLM?

Let's take the simple sentence:

**"The cat is sleeping."**

When we give this sentence to an LLM, it goes through several steps before generating an answer.

### Main Process

```text
Text
  ↓
Tokenization
  ↓
Tokens
  ↓
Token IDs
  ↓
Embeddings
  ↓
Transformer
  ↓
Next-token prediction
  ↓
Output
Step 1: Text

We start with:

The cat is sleeping.
Step 2: Tokenization

The LLM breaks the sentence into smaller pieces called tokens.

For example:

"The" | "cat" | "is" | "sleeping" | "."

The exact tokens can be different depending on the tokenizer.

Step 3: Token IDs

Each token is given a number called a Token ID.

For example, these numbers are only for understanding:

"The"       → 101
"cat"       → 245
"is"        → 56
"sleeping"  → 789
"."         → 12

So the sentence becomes:

[101, 245, 56, 789, 12]
Step 4: Embeddings

The token IDs are converted into embedding vectors.

For example:

cat
 ↓
Token ID: 245
 ↓
Embedding:
[0.21, -0.45, 0.73, 0.12, ...]

An embedding is a list of numbers that helps the model work with the information represented by the token.

Step 5: Transformer

The embeddings are processed by the Transformer.

The Transformer looks at the words and their relationships.

The → cat → is → sleeping
       ↑           ↑
       └───────────┘

It can understand from the context that "sleeping" is related to what the cat is doing.

Step 6: Next-token Prediction

The LLM predicts what token is likely to come next.

"The cat is sleeping."
          ↓
   What comes next?
          ↓
    Next token

The model calculates probabilities for possible next tokens and selects a token.

Complete Flow
"The cat is sleeping."
          ↓
    Tokenization
          ↓
["The", "cat", "is", "sleeping", "."]
          ↓
      Token IDs
          ↓
[101, 245, 56, 789, 12]
          ↓
     Embeddings
          ↓
     Transformer
          ↓
Next-token prediction
2. What is Tokenization, and why do LLMs need it?

Tokenization means breaking text into smaller pieces called tokens.

LLMs need tokenization because they process numbers rather than normal human-readable text.

Example 1: Common Word

Consider the word:

cat

It may be represented as one token:

"cat" → ["cat"]
Example 2: Long or Uncommon Word

Consider:

unbelievable

Depending on the tokenizer, it could be divided into smaller pieces such as:

"un" + "believ" + "able"

So:

unbelievable
      ↓
un | believ | able

The exact tokenization depends on the tokenizer.

Why do LLMs use tokens?

There are many words, names, technical terms, and combinations.

Instead of creating a separate token for every possible word, a tokenizer can break words into smaller reusable pieces.

Why is the number of tokens important?

The number of tokens is important because an LLM can process only a limited amount of text at one time.

For example:

Short text
    ↓
Fewer tokens
    ↓
Less processing

Whereas:

Long text
    ↓
More tokens
    ↓
More processing

The number of tokens can also affect the cost and speed when using an LLM through an API.

3. What is the difference between a Token ID and an Embedding?

A Token ID is a number used to identify a token.

An Embedding is a list of numbers used to represent information about that token.

Suppose:

cat → Token ID 1234
What does 1234 mean?

1234 is simply an identifier.

It tells the model which token is being used.

For example:

cat → 1234
dog → 5678
car → 9012

The numbers themselves do not contain the meaning of the words.

How is the Token ID converted into an Embedding?

The model has an embedding table.

Token ID
   ↓
  1234
   ↓
Embedding Table
   ↓
[0.21, -0.45, 0.73, 0.12, ...]

So:

cat
 ↓
1234
 ↓
[0.21, -0.45, 0.73, 0.12, ...]
Why can't we use 1234 to represent the meaning of "cat"?

Because 1234 is only an identifier.

For example:

cat → 1234
dog → 1235

The fact that the numbers are close does not mean that cat and dog have similar meanings.

Embeddings use many numbers and can represent useful relationships between words.

Difference
Token ID	Embedding
A single number	A list of numbers
Identifies a token	Represents information about a token
Example: 1234	Example: [0.21, -0.45, 0.73, ...]
4. How does an LLM generate an answer using next-token prediction?

An LLM generates text by predicting one token at a time.

Let's take:

The capital of India is
Step 1

The model predicts the next token.

The capital of India is
            ↓
          Delhi

Now the sentence becomes:

The capital of India is Delhi
Step 2

The model uses the updated sentence and predicts the next token.

The capital of India is Delhi
                    ↓
                    .

Now:

The capital of India is Delhi.
Complete Process
The capital of India is
            ↓
      Predict token
            ↓
          Delhi
            ↓
The capital of India is Delhi
            ↓
      Predict token
            ↓
            .
            ↓
The capital of India is Delhi.

The model continues this process until the answer is complete.

Another Simple Example
I am learning
      ↓
    Python
      ↓
I am learning Python
      ↓
 programming
      ↓
I am learning Python programming

So, next-token prediction means the model predicts the next token based on the tokens that came before it.

5. How do embeddings help an LLM understand relationships between words?

Embeddings represent words or tokens using vectors (lists of numbers).

Words that are used in similar situations can have similar embeddings.

For example:

        cat
         ●
        /
       /
      ● dog


                  ● car

Cat and dog may have similar embeddings because both are animals and can be pets.

Cat and car are usually less similar because they represent different things.

Example

The embeddings could look like:

cat → [0.80, 0.20, 0.75, ...]
dog → [0.78, 0.25, 0.72, ...]
car → [0.10, 0.90, 0.15, ...]

These numbers are only examples. Real embeddings contain many more numbers.

Cosine Similarity

Cosine similarity is one method used to compare two vectors.

It tells us how similar the directions of two vectors are.

The basic idea is:

Similar direction
       ↓
Higher similarity

Different direction
       ↓
Lower similarity

For example:

Similarity(cat, dog) = 0.90

Similarity(cat, car) = 0.20

These values are only examples.

This means:

cat ↔ dog
    ↓
More similar

cat ↔ car
    ↓
Less similar
Why is this useful?

Embedding similarity can help AI systems find related words, sentences, or information.

For example, a search for:

animals kept as pets

may find information about:

dogs
cats
rabbits

because their embeddings can be related to the meaning of the search.

Conclusion

The basic working of an LLM can be summarized as:

Text
 ↓
Tokenization
 ↓
Tokens
 ↓
Token IDs
 ↓
Embeddings
 ↓
Transformer
 ↓
Next-token prediction
 ↓
New token
 ↓
Repeat
 ↓
Answer

In simple words:

Tokenization breaks text into smaller pieces.
Token IDs give numbers to those pieces.
Embeddings represent tokens using vectors.
The Transformer processes the tokens and their context.
Next-token prediction allows the LLM to generate an answer one token at a time.
Similar embeddings can help the model understand relationships between words and concepts.

