# Social Media Content Generator 

### Install the requirements using pip

`pip install sentence-transformers chromadb groq langchain langchain-community langchain-groq pandas --q`

### Import the libraries that are necessary for the backend content generation using Langchain and llama

```import os
from langchain_groq import ChatGroq
from langchain_core.prompts import PromptTemplate
from langchain_core.output_parsers import StrOutputParser 
```
#### Additionally add getpass library
- This enables you to give input in run time <br>
`from getpass import getpass`

### Initialize the Groq API
- This makes you're app to have AI on the platform and It'll give output based on our prompt template

```
GROQ_API_KEY = os.environ.get('GROQ_API_KEY')
if not GROQ_API_KEY:
    GROQ_API_KEY = getpass('Enter your GROQ API key:')
    os.environ['GROQ_API_KEY'] = GROQ_API_KEY
```
### Initialize the LLM

`llm=ChatGroq(model="llama-3.3-70b-versatile")`

### Make the Prompt template
#### Made by Myself
   ```
   template="You are a Active social media content writer for various platform irrespective of the post content I need you to write a detailed content as user's wish in their style, platform such as Linkedin,Instagram,X,Reddit for which they have done things for example If User selects Linkedin/Instagram/X/Reddit, Long/short paragraph , needed/not-needed emoji, needed/not-needed hashtag the content should be given based on that"
   ``` 

#### Refined by ChatGPT

```
# Active Social Media Content Writer Prompt Template

## Role

You are an expert Social Media Content Writer and Personal Brand Strategist with experience creating high-performing content for LinkedIn, Instagram, X (Twitter), Reddit, Facebook, Threads, Medium, and other social platforms.

Your task is to create platform-native content that matches the user's tone, audience, goals, and writing style.

---

## User Inputs

### Platform

{Platform}

Examples:

* LinkedIn
* Instagram
* X (Twitter)
* Reddit
* Facebook
* Threads
* Medium

---

### Content Type

{Content_Type}

Examples:

* Achievement Post
* Project Showcase
* Product Launch
* Tutorial
* Storytelling
* Personal Experience
* Career Update
* Technical Explanation
* Event Recap
* Startup Journey
* Build In Public
* Educational Post
* Opinion Post
* Community Update

---

### Topic

{Topic}

---

### Context / Details

{Context}

Provide all relevant details including:

* What was built
* What was achieved
* Challenges faced
* Technologies used
* Results obtained
* Lessons learned
* Key takeaways

---

### Target Audience

{Target_Audience}

Examples:

* Recruiters
* Software Developers
* AI Engineers
* Startup Founders
* Students
* Data Scientists
* General Audience

---

### Tone

{Tone}

Examples:

* Professional
* Casual
* Friendly
* Inspirational
* Technical
* Educational
* Storytelling
* Humorous
* Confident
* Bold

---

### Length

{Length}

Options:

* Short
* Medium
* Long
* Detailed

---

### Emoji Usage

{Emoji_Usage}

Options:

* Required
* Not Required
* Minimal
* Heavy

---

### Hashtag Usage

{Hashtag_Usage}

Options:

* Required
* Not Required

If Required:
Generate highly relevant hashtags optimized for the selected platform.

---

### Call To Action

{CTA}

Examples:

* Ask for feedback
* Invite discussion
* Encourage sharing
* Request collaboration
* No CTA

---

### Writing Style

{Writing_Style}

Examples:

* Founder Style
* Corporate Style
* Creator Style
* Student Style
* Developer Style
* Researcher Style
* Influencer Style

---

## Instructions

Generate content that:

1. Follows platform-specific best practices.
2. Matches the selected tone and style.
3. Sounds natural and human-written.
4. Avoids generic AI phrases.
5. Uses storytelling when appropriate.
6. Creates a strong hook within the first 1–3 lines.
7. Maintains readability with proper spacing.
8. Uses platform-native formatting.
9. Highlights achievements without sounding arrogant.
10. Optimizes engagement for the selected platform.
11. Includes relevant hashtags only if requested.
12. Includes emojis only if requested.
13. Includes a CTA only if requested.
14. Ensures authenticity and credibility.
15. Makes readers want to engage, comment, or share.

---

## Platform-Specific Rules

### LinkedIn

* Strong professional hook.
* Use short paragraphs.
* Focus on journey, lessons, impact, and results.
* Professional storytelling.
* End with a thoughtful question or CTA if requested.

### Instagram

* Attention-grabbing first line.
* Conversational and engaging.
* Emotional or relatable storytelling.
* Suitable for captions.
* Include hashtag section if requested.

### X (Twitter)

* Concise and impactful.
* Hook immediately.
* Optimize for reposts and engagement.
* Use thread format when content is long.

### Reddit

* Authentic and community-focused.
* Avoid promotional language.
* Prioritize value and discussion.
* Match subreddit culture.
* Sound like a real community member.

### Facebook

* Conversational and community-oriented.
* Focus on storytelling and engagement.

### Medium

* Long-form structured article.
* Use headings and subheadings.
* Educational and informative.

---

## Output Format

### Content

[Generated Content]

### Suggested Hook Variations

1. ...
2. ...
3. ...

### Hashtags

[Only if requested]

### Engagement Score Strategy

* Why this content works
* Expected audience reaction
* Engagement optimization techniques used
```

### Intialize the parser
`parser=StrOutputParser()`

### Make the chain of the prompt, llm and parser

`chain=prompt |llm|parser`

### Get the response

`response = chain.invoke({
    "Platform": "LinkedIn",
    "Content_Type": "Project Showcase",
    "Topic": "Calculator App using Streamlit",
    "Context": "Built a calculator that accepts multiple inputs and performs arithmetic operations using Streamlit.",
    "Target_Audience": "Software Developers",
    "Tone": "Professional",
    "Length": "Long",
    "Emoji_Usage": "Minimal",
    "Hashtag_Usage": "Required",
    "CTA": "Ask for feedback",
    "Writing_Style": "Developer Style"
})`

#### The output for the response is

```
Content

As a software developer, I'm excited to share my recent project, a calculator app built using Streamlit, which accepts multiple inputs and performs arithmetic operations. The goal was to create a user-friendly interface that simplifies complex calculations, making it easier for users to focus on their work.

The project began with researching the capabilities of Streamlit, a Python library that allows developers to create web apps with a simple and intuitive syntax. I was impressed by its ease of use and the ability to create interactive dashboards. With this knowledge, I designed the calculator app to handle multiple inputs, perform calculations, and display the results in a clear and concise manner.

One of the challenges I faced was handling errors and exceptions. To address this, I implemented a robust error handling system that provides informative error messages, helping users understand what went wrong and how to correct it. This not only improved the user experience but also made the app more reliable.

The technologies used in this project include Streamlit, Python, and various libraries for handling calculations and data processing. By leveraging these tools, I was able to create a high-quality app that meets the needs of users. The results obtained were impressive, with the app performing calculations accurately and efficiently.

Throughout this project, I learned several valuable lessons. First, the importance of testing and debugging cannot be overstated. Thorough testing helped me identify and fix issues, ensuring the app was stable and reliable. Second, I realized the value of using existing libraries and frameworks, which saved time and effort. Finally, I understood the need for clear and concise documentation, which facilitated the development process and made it easier for others to understand the code.

The key takeaways from this project are the power of Streamlit in creating interactive web apps, the importance of robust error handling, and the value of leveraging existing libraries and frameworks. By applying these principles, developers can create high-quality apps that meet the needs of users and provide a positive user experience.

As I look back on this project, I'm proud of what I've accomplished and the skills I've developed. I'm eager to hear your thoughts and feedback on this project. What do you think about using Streamlit for building web apps? Have you worked on any similar projects?

Suggested Hook Variations

1. "I'm thrilled to share my latest project, a calculator app built with Streamlit, which is revolutionizing the way we perform calculations."
2. "As a software developer, I'm always looking for ways to simplify complex tasks, which is why I created a calculator app using Streamlit."
3. "Streamlit has been making waves in the development community, and I'm excited to share my experience with building a calculator app using this powerful tool."

Hashtags

#Streamlit #CalculatorApp #SoftwareDevelopment #WebApp #Python #ErrorHandling #UserExperience #DeveloperCommunity #Coding #Programming #AppDevelopment #TechInnovation

Engagement Score Strategy

* Why this content works: The content is engaging because it shares a personal experience, highlights the benefits of using Streamlit, and asks for feedback, encouraging discussion and interaction.
* Expected audience reaction: The audience is expected to be interested in the project, ask questions, and share their own experiences with Streamlit or similar technologies.
* Engagement optimization techniques used: The content uses a strong professional hook, short paragraphs, and a clear structure to maintain readability. The use of relevant hashtags and a call-to-action (asking for feedback) also optimize engagement. Additionally, the content highlights achievements without sounding arrogant, making it more relatable and authentic.
```
---
### Now I need to connect this in Gradio
`pip install gradio`
`import gradio as gr`

#### Add these below the `chain = prompt | llm | parser`

```
def generate_content(
    Platform,
    Content_Type,
    Topic,
    Context,
    Target_Audience,
    Tone,
    Length,
    Emoji_Usage,
    Hashtag_Usage,
    CTA,
    Writing_Style
):

    response = chain.invoke({
        "Platform": Platform,
        "Content_Type": Content_Type,
        "Topic": Topic,
        "Context": Context,
        "Target_Audience": Target_Audience,
        "Tone": Tone,
        "Length": Length,
        "Emoji_Usage": Emoji_Usage,
        "Hashtag_Usage": Hashtag_Usage,
        "CTA": CTA,
        "Writing_Style": Writing_Style
    })

    return response


custom_css = """
.gradio-container {
    max-width: 1200px !important;
    margin: auto !important;
}

footer {
    display: none !important;
}
"""


with gr.Blocks(
    title="Social Media Content Generator",
    theme=gr.themes.Monochrome(),
    css=custom_css
) as demo:

    gr.Markdown("# Social Media Content Generator")
    gr.Markdown("Generate platform-specific social media content.")

    with gr.Row():
        Platform = gr.Dropdown(
            ["LinkedIn", "Instagram", "X", "Reddit", "Facebook"],
            label="Platform"
        )

        Content_Type = gr.Dropdown(
            [
                "Achievement Post",
                "Project Showcase",
                "Product Launch",
                "Tutorial",
                "Storytelling",
                "Personal Experience",
                "Career Update",
                "Technical Explanation",
                "Event Recap",
                "Startup Journey",
                "Build In Public",
                "Educational Post",
                "Opinion Post",
                "Community Update"
            ],
            label="Content Type"
        )

    Topic = gr.Textbox(
        label="Topic",
        placeholder="Enter your topic"
    )

    Context = gr.Textbox(
        label="Context / Details",
        lines=8,
        placeholder="Describe your project, achievement, experience, etc."
    )

    with gr.Row():
        Target_Audience = gr.Textbox(
            label="Target Audience"
        )

        Tone = gr.Dropdown(
            [
                "Professional",
                "Casual",
                "Friendly",
                "Inspirational",
                "Technical",
                "Educational",
                "Storytelling",
                "Humorous",
                "Confident",
                "Bold"
            ],
            label="Tone"
        )

    with gr.Row():

        Length = gr.Dropdown(
            ["Short", "Medium", "Long", "Detailed"],
            label="Length"
        )

        Emoji_Usage = gr.Dropdown(
            ["Required", "Minimal", "Heavy", "Not Required"],
            label="Emoji Usage"
        )

        Hashtag_Usage = gr.Dropdown(
            ["Required", "Not Required"],
            label="Hashtag Usage"
        )

    CTA = gr.Textbox(
        label="Call To Action"
    )

    Writing_Style = gr.Dropdown(
        [
            "Founder Style",
            "Corporate Style",
            "Creator Style",
            "Student Style",
            "Developer Style",
            "Researcher Style",
            "Influencer Style"
        ],
        label="Writing Style"
    )

    generate_btn = gr.Button(
        "Generate Content",
        variant="primary"
    )

    output = gr.Markdown(
        label="Generated Content"
    )

    generate_btn.click(
        fn=generate_content,
        inputs=[
            Platform,
            Content_Type,
            Topic,
            Context,
            Target_Audience,
            Tone,
            Length,
            Emoji_Usage,
            Hashtag_Usage,
            CTA,
            Writing_Style
        ],
        outputs=output
    )
```

#### Run the app
demo.launch(share=True)
- share=True enables to make the URL public

#### PUBLIC [LINK](https://9dd8aa977910219dc9.gradio.live/) 