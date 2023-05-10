# promptmaster
💬 Best practices for prompting using the OpenAI API.

## Prompting Principles
**Principle 1**: Write clear and specific instructions
   * `clear != short` 
   * Longer prompts can be more specific

Tactic 1: **Use delimiters**
```
triple quotes: """
tripe dashes: ---
Angle brackets: <>
XML
```

Tactic 2: **Few shot prompting**
```py
prompt = f"""
Your task is to answer in a consistent style, use analogies and emojis at the end of the line.

<child>: Teach me about patience.

<grandparent>: 
The river that carves the deepest 🏞️ \  
valley flows from a modest spring; 🌊 \   
the grandest symphony originates from a single note; 🎵 \  
the most intricate tapestry begins with a solitary thread. 🧵 \  

<child>: Teach me about rebellion against authority.
"""
response = get_completion(prompt, model="gpt-4", temperature=0.7)
print(response)
```
Response:
> \<grandparent>  
> A tiny seed can sprout into a tree, breaking through concrete; 🌱 \
a river can change its course, defying the landscape; ⛰️ \
a single spark can ignite a wildfire, sweeping through a forest. 🔥 

</br>

**Principle 2**: Give the model time to “think”
* i.e. Specify the **steps required** to complete a task
```py
text = f"In a charming village, siblings Jack and Jill..."

prompt = f""" Perform the following actions: 
1 - Summarize the following text delimited by triple brackets \
        in 1 sentence.
2 - Translate the summary into French.
3 - List each name in the French summary.
4 - Output a json object that contains the following \
        keys: french_summary, num_names.

Separate your answers with line breaks.

Text:
<<<{text}>>>
"""
```

**Principle 3**  Ask the model to check conditions are satisfied
* i.e. "Follow these instructions, if you cannot then respond with a specific message"
```py
"""
…
If the text does not contain a sequence of instructions, \ 
then simply write \"No steps provided.\"

\"\"\"{text}\"\"\"
"""
```

