1. What happens when we give a sentence to an LLM?

Let's take the sentence:

"The cat is sleeping."

When we give this sentence to an LLM, it does not directly understand the sentence like a human. The text goes through several steps.

Main process
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

"The cat is sleeping."
Step 2: Tokenization

The LLM breaks the sentence into smaller pieces called tokens.

For example, a tokenizer might produce:

"The"  "cat"  "is"  "sleeping"  "."

The exact tokens can be different depending on the tokenizer.

Step 3: Token IDs

The model's vocabulary assigns a numerical ID to each token.

For example, these numbers are only illustrative:

"The"       →  101
"cat"       →  2457
"is"        →  200
"sleeping"  →  5832
"."         →  15

So the sentence becomes:

[101, 2457, 200, 5832, 15]
Step 4: Embeddings

The token IDs themselves do not contain meaning.

The model uses each ID to look up a numerical vector called an embedding.

For example:

"cat" → Token ID 2457
          ↓
     Embedding
          ↓
[0.21, -0.45, 0.73, 0.12, ...]

The real embedding contains many more numbers.

These numbers help the model represent relationships and meaning.

Step 5: Transformer

The embeddings are processed by the Transformer.

The Transformer uses mechanisms such as attention to determine how words relate to each other.

For example:

The → cat → is → sleeping
       ↑           ↑
       └── meaning ┘

The model can use the surrounding words to understand that "sleeping" describes what the cat is doing.

Step 6: Next-token prediction

The LLM predicts what token is likely to come next.

For example:

"The cat is sleeping."
                 ↓
          What comes next?
                 ↓
                ...

The model calculates probabilities for possible next tokens.

"Today"    → 0.02
"The"      → 0.01
"."        → 0.40
"\n"       → 0.10
...

The exact probabilities depend on the model and context.

Complete flow
"The cat is sleeping."
          ↓
     Tokenization
          ↓
["The", "cat", "is", "sleeping", "."]
          ↓
     Token IDs
          ↓
[101, 2457, 200, 5832, 15]
          ↓
     Embeddings
          ↓
   Transformer
          ↓
Next-token probabilities
          ↓
   Predicted token
2. What is tokenization, and why do LLMs need it?

Tokenization is the process of breaking text into smaller pieces called tokens.

Computers cannot directly process a sentence as human-readable text. LLMs convert the text into tokens and then numbers.

Example 1: Common word

Consider:

cat

A tokenizer may represent it as one token:

"cat" → ["cat"]

Another tokenizer could use a different representation, but common words are often single tokens.

Example 2: Long or uncommon word

Consider:

unbelievable

Depending on the tokenizer, it might be split into pieces such as:

"un" + "believ" + "able"

So:

unbelievable
      ↓
["un", "believ", "able"]

This allows the model to handle words it has not frequently encountered as complete words.

Why not store every possible word?

There are an enormous number of words, names, technical terms, spellings and combinations.

Instead of having one token for every possible word, tokenizers can reuse smaller pieces.

For example:

play
player
playing
playful

may share parts related to:

play

This makes the vocabulary more manageable.

Why is the number of tokens important?

LLMs have a limit on how much text they can process at once. This is related to the model's context window.

For example:

Short sentence
     ↓
Few tokens
     ↓
Less context used

while:

Long document
     ↓
Many tokens
     ↓
More context used

The number of tokens can also affect cost and processing time when using an LLM API.

Simple diagram
Sentence
   ↓
Tokenizer
   ↓
┌──────┬──────┬──────┬───────┐
│ The  │ cat  │ is   │ sleep │
└──────┴──────┴──────┴───────┘
   ↓
Token IDs
   ↓
Numbers
3. Difference between Token ID and Embedding

A Token ID and an Embedding are two different things.

Suppose the word:

cat

is converted into:

Token ID = 1234
What does 1234 mean?

The number 1234 is simply an identifier.

It tells the model:

"The token at vocabulary position 1234 is this particular token."

It does not mean that 1234 represents the meaning or characteristics of a cat.

Think of it like a student ID:

Student name → Rahul
Student ID   → 1234

The number 1234 identifies the student, but it doesn't describe the student's personality, skills, or appearance.

Similarly:

"cat" → 1234

The ID identifies the token.

From Token ID to Embedding

The model has an embedding table.

Conceptually:

             Embedding Table
          ┌─────────────────────┐
ID 1233 → │ [.... .... ....]    │
ID 1234 → │ [0.21, -0.45, ...]  │ ← cat
ID 1235 → │ [.... .... ....]    │
          └─────────────────────┘
                    ↓
             Embedding vector

So:

cat
 ↓
1234
 ↓
[0.21, -0.45, 0.73, 0.12, ...]
Why can't we use 1234 directly?

Because the number 1234 doesn't contain semantic information.

For example:

cat → 1234
dog → 5678
car → 9101

The numerical difference between these IDs doesn't tell us how similar the meanings are.

For example:

5678 - 1234 = 4444

That does not mean dog is "4444 units" away from cat in meaning.

Embeddings are designed to represent useful patterns and relationships in a high-dimensional vector space.

Simple comparison
Token ID	Embedding
Identifier	Numerical representation
Usually one integer	Vector containing many numbers
Identifies a token	Helps represent information about the token
Example: 1234	Example: [0.21, -0.45, 0.73, ...]
4. How does an LLM generate an answer using next-token prediction?

LLMs generate text one token at a time.

Consider:

"The capital of India is"

The model receives this sequence and predicts what token should come next.

Step 1

Input:

The capital of India is

The model predicts possible next tokens.

For example:

Delhi   → high probability
Mumbai  → lower probability
Chennai → lower probability
...

The model selects a token, such as:

Delhi

Now the sequence becomes:

The capital of India is Delhi
Step 2

The model uses the updated sequence:

The capital of India is Delhi

and predicts the next token.

It might predict:

"." 

Now:

The capital of India is Delhi.
Step 3

The model checks whether it should continue generating.

If it generates an ending token, the generation stops.

Complete process
"The capital of India is"
              ↓
       Predict next token
              ↓
           "Delhi"
              ↓
"The capital of India is Delhi"
              ↓
       Predict next token
              ↓
             "."
              ↓
"The capital of India is Delhi."

The important idea is:

The model repeatedly predicts the next token based on all the tokens that came before it.

Another example
Input:
"I like eating"

        ↓

Prediction:
"pizza"

        ↓

"I like eating pizza"

        ↓

Prediction:
"because"

        ↓

"I like eating pizza because"

        ↓

Prediction:
"it"

        ↓

"I like eating pizza because it ..."

This process continues until the model reaches a stopping condition or a maximum token limit.

5. How do embeddings help an LLM understand relationships between words?

Embeddings represent tokens as vectors.

Words with related meanings or usage can have embeddings that are closer together in the vector space.

For example:

             cat
              ●
             /
            /
           ● dog


                         ● car

Here, cat and dog may be closer because they are both animals and often appear in similar contexts.

Cat and car may be less similar because they usually represent very different concepts.

Important: embeddings do not literally contain dictionary definitions. Their relationships are learned from how words and tokens are used in large amounts of text.

Example

Conceptually:

cat → [0.80, 0.20, 0.75, ...]
dog → [0.78, 0.25, 0.72, ...]
car → [0.10, 0.90, 0.15, ...]

The actual values are much larger vectors and are learned by the model.

Cosine Similarity

One common way to compare two vectors is cosine similarity.

It measures how similar the direction of two vectors is.

The formula is:

$$ \text{Cosine Similarity}(A,B) = \frac{A\cdot B}{\|A\|\|B\|} $$

The basic idea is:

Very similar direction
       ↘     ↙
        \   /
         \ /
          ●

If two vectors point in nearly the same direction, their cosine similarity is close to 1.

If they are very different, the similarity can be closer to 0 (for typical semantic embedding comparisons).

Example

Suppose:

Similarity(cat, dog) = 0.90
Similarity(cat, car) = 0.25

These numbers are only illustrative.

This would suggest:

cat ↔ dog
High similarity

cat ↔ car
Lower similarity
Why is this useful?

Embedding similarity can help systems find related information.

For example, if someone searches:

"animals that are good pets"

the system can use embeddings to find text containing related concepts such as:

dogs
cats
rabbits
pets

even when the exact words are not identical.

Overall Summary

The five concepts are connected:

                 USER INPUT
                     │
                     ▼
              "The cat sleeps"
                     │
                     ▼
                TOKENIZATION
                     │
                     ▼
            ["The","cat","sleeps"]
                     │
                     ▼
                 TOKEN IDs
                     │
                     ▼
              EMBEDDING VECTORS
                     │
                     ▼
                TRANSFORMER
                     │
                     ▼
          NEXT-TOKEN PREDICTION
                     │
                     ▼
              "The cat sleeps."
                     │
                     ▼
          Repeat until completion
In simple words
Tokenization breaks text into manageable pieces.
Token IDs give each token a numerical identifier.
Embeddings convert those tokens into vectors that can represent useful relationships.
The Transformer processes these vectors and their context.
The LLM performs next-token prediction repeatedly to generate an answer.
Similar concepts can have similar embeddings, which helps the model work with relationships between words and ideas.

This is a good structure for your Assignment-2 README/documentation and is suitable for uploading to your GitHub repository.#   A s s i g n m e n t - 2  
 