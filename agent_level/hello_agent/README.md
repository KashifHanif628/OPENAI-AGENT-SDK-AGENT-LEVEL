# Agent-Level Configuration ka matlab:
Aap ek aise "agent" (yaani assistant/chatbot) bana rahe hain jo Google Gemini model ka use karega, OpenAI ke default model ke bajaye.

Yeh sirf ek agent ke liye Gemini use karta hai. Baaki agents agar honge to woh OpenAI default se chalenge.


# Code Clarification

# import asyncio
📌 Python ka ek module jo async code chalane ke liye use hota hai (yaani code jo ruk ruk ke background me kaam kare).


# from dotenv import load_dotenv
# import os
 📌 Yeh dono lines .env file se Gemini ki API key ko environment variable ke zariye read karte hain.

.env file me likha hota hai:
GEMINI_API_KEY=your_key_here

load_dotenv() us file ko read karta hai.
os.getenv("GEMINI_API_KEY") se key milti hai.


# from openai import AsyncOpenAI
# from agents import Agent, OpenAIChatCompletionsModel, Runner, set_tracing_disabled
📌 Yeh Agents SDK ke tools ko import kar rahe hain:

# Agent: Aapka chatbot.
# OpenAIChatCompletionsModel: Yeh model ka reference hai — hum isme Gemini dene wale hain.
# Runner: Yeh agent ko run karne ka system hai.
# set_tracing_disabled: Tracing disable karne ke liye (tracing ek tracking feature hota hai).



# load_dotenv()
# gemini_api_key = os.getenv("GEMINI_API_KEY")
📌 Yeh dono lines .env file me se Gemini ki API key nikal kar variable gemini_api_key me store karti hain.


client = AsyncOpenAI(
    api_key=gemini_api_key,
    base_url="https://generativelanguage.googleapis.com/v1beta/openai/",
)
📌 Yeh line ek Gemini client banata hai, jiske through hum Gemini model se baat karenge.
api_key: aapki Gemini ki key hai
base_url: Gemini API ka address


# set_tracing_disabled(disabled=True)
📌 Yeh line tracking system ko band kar deti hai — zaroori nahi hoti, sirf background data logging ke liye hoti hai.


# async def main():
📌 Yeh ek main function hai jo async hai — kyun? Kyunki hum background me Gemini se message bhej rahe hain aur uska reply le rahe hain.



    agent = Agent(
        name="Assistant",
        instructions="You only respond in haikus.",
        model=OpenAIChatCompletionsModel(model="gemini-2.0-flash", openai_client=client),
    )
📌 Yahaan ek chatbot (agent) ban raha hai:
name: is agent ka naam
instructions: yeh agent kya kare — yahaan usse kaha gaya ke sirf haiku (Japanese short poem) me reply kare.
model: Gemini model use ho raha hai "gemini-2.0-flash" ka, jo client me diya gaya.



    result = await Runner.run(
        agent,
        "Tell me about recursion in programming.",
    )
📌 Yeh agent se ek message bhej raha hai: "recursion kya hoti hai?"
await ka matlab: ruk kar Gemini ka jawaab milne ka intezaar karo.



#    print("👉 Agent-Level Response:\n", result.final_output)
📌 Jab agent reply de deta hai, to uska final answer print ho jata hai.



if __name__ == "__main__":
    asyncio.run(main())
📌 Yeh standard Python syntax hai — yeh kehta hai ke jab aap script chalayen, to main() function start ho jaye.



# command chalayenge:

uv run main_agent.py
Aur output me kuch aisa milega:

# Output
👉 Agent-Level Response:
A function calls self—
nested layers deep within,
code that loops in peace.


✅ Summary (Aasan Zubaan Me)
Cheez	Matlab
Agent	Aapka assistant/chatbot
Runner.run()	Yeh agent se sawaal karne aur jawab lene ka tareeqa hai
model="gemini..."	Aap OpenAI ke bajaye Gemini model use kar rahe hain
.env file	API key secure rakhne ka tareeqa
uv run	Script chalane ka tareeqa