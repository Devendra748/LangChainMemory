# LangChain Memory
This README provides an overview and examples of how to use the LangChain library. LangChain is a Python library that enables easy integration with OpenAI's GPT-3.5 language model for conversational AI tasks. It provides various memory mechanisms to store and retrieve conversation history, allowing the model to have context-aware interactions.

## Installation
To use LangChain, you need to have Python installed on your system. You can install LangChain using pip:
**pip install langchain**

## Usage
```
To use LangChain, you need to import the required modules and set up your OpenAI API key:
import os
from dotenv import load_dotenv, find_dotenv
_ = load_dotenv(find_dotenv())  # Read local .env file

from langchain.chat_models import ChatOpenAI
from langchain.chains import ConversationChain
from langchain.memory import ConversationBufferMemory

os.environ["OPENAI_API_KEY"] = "YOUR_OPENAI_API_KEY"

llm = ChatOpenAI(temperature=0.0)
memory = ConversationBufferMemory()
conversation = ConversationChain(
    llm=llm,
    memory=memory,
    verbose=True
)

response = conversation.predict(input="Hi, my name is Devendra")
print(response)
```
This sets up the LangChain library, initializes the ChatOpenAI model, creates a conversation buffer memory, and starts a conversation with an initial input. The conversation.predict method returns the model's response, which can be printed or used in further processing.

## Memory Mechanisms
LangChain provides several memory mechanisms to store and retrieve conversation history. Here are some examples:

## ConversationBufferMemory
```
from langchain.memory import ConversationBufferMemory

memory = ConversationBufferMemory()
memory.save_context({"input": "Hi"}, {"output": "What's up"})
memory.save_context({"input": "Not much, just hanging"}, {"output": "Cool"})

print(memory.buffer)
```
The ConversationBufferMemory stores conversation history in a buffer. You can save conversation context using the save_context method and retrieve the buffer using the buffer attribute.

## ConversationBufferWindowMemory
```
from langchain.memory import ConversationBufferWindowMemory

memory = ConversationBufferWindowMemory(k=1)
memory.save_context({"input": "Hi"}, {"output": "What's up"})
memory.save_context({"input": "Not much, just hanging"}, {"output": "Cool"})

print(memory.buffer)
```
The ConversationBufferWindowMemory is similar to ConversationBufferMemory, but it only keeps the latest k turns of conversation history.

## ConversationTokenBufferMemory
```
from langchain.memory import ConversationTokenBufferMemory
from langchain.llms import OpenAI

llm = ChatOpenAI(temperature=0.0)
memory = ConversationTokenBufferMemory(llm=llm, max_token_limit=30)
memory.save_context({"input": "AI is what?!"}, {"output": "Amazing!"})
memory.save_context({"input": "Backpropagation is what?"}, {"output": "Beautiful!"})

print(memory.buffer)
```
The ConversationTokenBufferMemory stores conversation history based on the number of tokens used. It can be useful when you want to limit the memory based on token count.

## ConversationSummaryBufferMemory
```
from langchain.memory import ConversationSummaryBufferMemory

memory = ConversationSummaryBufferMemory(llm=llm, max_token_limit=100)
memory.save_context({"input": "Hello"}, {"output": "What's up"})

print(memory.buffer)
```
The ConversationSummaryBufferMemory stores conversation history in a summarized format, providing an overview of the. Click View entire message to view it.
