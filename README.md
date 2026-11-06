Link to add to Google Colab: https://colab.research.google.com/github/mbentogyo/iaproj/blob/master/quiz-presentation-generator.ipynb

# **Presentation Quiz Generator**
This system is a Google Colab application that utilizes a 4-bit quantized 7-billion parameter local language model to generate multiple-choice questions from user-provided text. The output is programmatically formatted into a PowerPoint presentation file.

# Hardware Requirements
You must run this system on a hardware-accelerated environment. The system will fail if executed on a standard CPU instance.
*   Navigate to **Runtime > Change runtime type**.
*   Select the **T4 GPU** and press save.

# Execution Architecture
The code is intentionally separated into two distinct execution blocks to optimize memory allocation and reduce latency. 
1. Run the first cell to install necessary dependencies and load the model weights into the GPU Video RAM. Do this only ONCE per session.
    - Note: Execution time is dependent on network speed for the initial model download.
2. The second cell handles user input, model inference, JSON parsing, and slide generation. You can execute this cell how many times necessary to get outputs.
    - It will ask the user to input 3 things: Quiz Title, Lesson Text, and Number of Questions.

# Output Specifications
The system automatically downloads two files to the local machine upon completion:

* Raw Text File (.txt): Contains the raw JSON output from the language model. This serves as a diagnostic log if the parsing fails.

* Presentation File (.pptx): The finalized quiz presentation.

# Presentation Formatting Logic
The generated PowerPoint file adheres to the following structural rules:

* The aspect ratio follows a 4:3 layout.
* Each question generated will have a single page, which also contains the four choices.
* Font sizes for questions and choices adjust based on total character count to prevent text truncation. Limits are 32pt for standard text, 26pt for text exceeding 350 characters, and 20pt for text exceeding 600 characters.
* The answers are grouped 10 per slide using a two-column layout. The left column holds items 1 through 5, and the right column holds items 6 through 10. The font is statically sized at 54pt.

# Troubleshooting
If the system returns an error stating the model did not return a valid format, inspect the downloaded text file. This indicates the language model failed to adhere to the strict JSON schema. Rerunning Cell 2 will typically resolve this due to the stochastic nature of the generation process.
