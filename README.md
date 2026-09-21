# FTEC5660 Homework 1: Receipt Chain

Build a LangChain pipeline that reads every supermarket receipt in a folder
with the vision-capable DeepSeek Flash model and answers these two questions:

1. How much money did I spend in total for these bills?
2. How much would I have had to pay without the discount?

For this homework, **amount spent** means the final payment after the receipt's
rounding line. **Without the discount** means the sum of the original positive
item prices: add back every promotion, coupon, member, app, packaging-damage,
and percentage discount, but do not add back rounding.

## Student task

Only edit the two functions in `hw1.py` that contain `### YOUR CODE HERE`:

- `build_chain()` creates your LangChain chain.
- `answer_queries()` runs the chain on the receipt images and returns one final
  response for each question.

You may use prompt chaining, routing, parallel calls, reflection, or a
combination. Your final responses should each contain one HKD amount. Do not
hard-code filenames or public answers; grading uses unseen receipt folders.

## Setup and public test

```bash
python3 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

Put your DeepSeek key after `DEEPSEEK_API_KEY=` in `.env`, then run:

```bash
python3 hw1.py --image-folder public_test
```

The program creates `results.csv` in the current directory. Its columns are
`query`, `model_response`, and `correctness`. The public answers are in
`public_test/ground_truth.json`. The starter intentionally returns the dummy
response `please design your chain to answer these two queries.` so it runs
before you add any API code.

The required model is `deepseek-v4-flash-vision-exp`, the vision-capable
DeepSeek Flash model. JPEG, PNG, GIF, and WebP inputs are accepted by the
homework runner.


## Homework 1 solution: 
> to students: please fill your solution description here.

## Chain Visualization
```
    +-------------+
    | PromptInput |
    +-------------+
           *
           *
           *
+--------------------+
| ChatPromptTemplate |
+--------------------+
           *
           *
           *
   +--------------+
   | ChatDeepSeek |
   +--------------+
           *
           *
           *
+--------------------+
| ChatDeepSeekOutput |
+--------------------+

## Solution Description
``` In this assignment, I broke down the task into two steps: data extraction and data calculation. During the construction of the build_chain function, I called functions from the LangChain module and relied on deepseek-v4-flash-vision-exp for data extraction. I designed a prompt to ensure that the model retains only the numbers and currency symbols while reading the data, and defined the input format for the model, namely image-form receipts and text-form questions, to facilitate the next step of calculation. In the construction of the answer_queries function, I used for loops and if conditional statements to ensure that all input image information could be fully processed. I defined q1 and q2 corresponding to the two questions posed in the assignment, and used the Decimal function to complete the summation, ensuring two decimal places are retained in the final data output stage to prevent floating-point errors. Through this assignment, I consolidated the concepts covered in the first two weeks of lectures through hands-on practice, which also gave me a preliminary understanding and insight into the practical applications of AI Agents.
Notably, the Chain Visualization section was also generated using Python, and the code used is:
from hw1 import load_env_file, build_chain
load_env_file()  
chain = build_chain()
print(chain.get_graph().print_ascii())