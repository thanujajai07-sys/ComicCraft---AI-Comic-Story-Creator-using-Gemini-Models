# ComicCraft---AI-Comic-Story-Creator-using-Gemini-Models
ComicCraft — AI-Powered Comic Generator

ComicCraft is an AI-based web application that converts a simple story concept into a complete five-frame comic. It uses Gemini to develop the storyline and dialogue, while Stable Diffusion generates artwork for each scene. The finished comic can be viewed online and saved as a PDF.

Project Workflow

ComicCraft creates a comic through the following stages:

1. Create the Plot
   Gemini generates a five-scene storyline based on the user's idea. Each scene also receives a suitable prompt for image generation.

2. Develop the Story
   Gemini expands the generated outline by adding narration, captions, and character conversations.

3. Generate Artwork
   Stable Diffusion creates an image for every comic panel. The generated images are stored inside the application's panel directory. A placeholder mode is also available for testing without downloading the image-generation model.

4. Build the Comic and PDF
   The five panels are arranged into a comic layout and converted into a downloadable PDF using FPDF2.

Technologies Used

The project is built using:

- FastAPI — Backend web framework
- Jinja2 — HTML template rendering
- Google GenAI — Story and text generation
- Hugging Face Diffusers — AI image generation
- Transformers & PyTorch — Machine-learning support
- Pillow — Image processing
- FPDF2 — PDF creation

System Requirements

Before running the application, make sure you have:

- Python 3.11 or later
- A valid Gemini API key
- Sufficient storage for the image-generation model
- An NVIDIA GPU is recommended when using Stable Diffusion for faster image creation

Installation

Windows PowerShell

Open PowerShell and run:

cd ComicCraft
py -m venv .venv
.venv\Scripts\activate
python -m pip install --upgrade pip
pip install -r requirements.txt
copy .env.example .env

After creating the ".env" file, enter your Gemini API key in:

GEMINI_API_KEY=your_api_key

Keep the ".env" file private because it contains sensitive configuration information.

Running the Application Without Image Generation

For a quick test, you can avoid downloading the Stable Diffusion model.

Set the following value in ".env":

IMAGE_PROVIDER=placeholder

Then launch the application:

python -m app.main

The server will normally be available at:

http://127.0.0.1:8000/

You can also start the application using:

uvicorn app.main:app --reload

Enabling AI Image Generation

To generate actual comic artwork, change the image provider:

IMAGE_PROVIDER=diffusers

During the first image-generation request, the configured Stable Diffusion model will be downloaded. This can require several gigabytes of storage.

For NVIDIA GPU systems, installing a CUDA-supported PyTorch version can significantly improve generation speed.

You can verify GPU availability with:

python -c "import torch; print(torch.cuda.is_available())"

If the selected Hugging Face model requires authentication, provide the token through:

HF_TOKEN=your_token

Application Configuration

The main settings can be controlled through the ".env" file.

Setting| Default| Description
"GEMINI_API_KEY"| —| API key required for Gemini
"GEMINI_OUTLINE_MODEL"| "gemini-3.8-flash"| Creates the comic outline
"GEMINI_STORY_MODEL"| "gemini-3.1-pro-preview"| Produces narration and dialogue
"GEMINI_FALLBACK_MODEL"| Empty| Optional backup Gemini model
"IMAGE_PROVIDER"| "diffusers"| Selects AI images or placeholders
"IMAGE_MODEL_ID"| Stable Diffusion 1.5| Model used for artwork
"IMAGE_STEPS"| "20"| Number of diffusion steps
"IMAGE_WIDTH"| "512"| Generated image width
"IMAGE_HEIGHT"| "512"| Generated image height
"SEED"| "42"| Starting value used for reproducible images
"HF_TOKEN"| Empty| Hugging Face authentication token
"APP_HOST"| "127.0.0.1"| Server host
"APP_PORT"| "8000"| Server port
"DEBUG"| "true"| Enables development/reload mode

AI model names may change over time. If a configured Gemini model is unavailable, replace it with a currently supported model.

Available API Routes

Method| Endpoint| Function
"GET"| "/"| Opens the comic generator interface
"POST"| "/generate"| Creates a comic through the web form
"POST"| "/generate-comic/json"| Generates comic information through JSON
"POST"| "/export-json"| Creates a PDF from an existing comic layout
"GET"| "/download/{filename}"| Downloads a generated PDF
"POST"| "/test-image"| Creates an image from a supplied prompt
"GET"| "/docs"| Opens the Swagger API documentation

Sample JSON Request

{
  "story_prompt": "A young explorer discovers a hidden city.",
  "character_name": "Maya",
  "setting": "Ancient city",
  "tone": "Adventurous",
  "art_style": "Graphic novel"
}

The application accepts panel images only from the designated panel directory when exporting a comic. PDF downloads are also restricted to generated files in the export directory.

Testing the Project

For a basic test:

1. Add a valid Gemini API key.
2. Set "IMAGE_PROVIDER=placeholder".
3. Start the application.
4. Open the web interface.
5. Enter a story idea and submit it.
6. Confirm that five comic panels are displayed.
7. Test the Download PDF option.

The API can also be tested through the Swagger interface at "/docs".

Common Problems

Package installation error

If dependency installation reports a version conflict, check that the versions listed in "requirements.txt" are compatible with the installed Python environment.

Gemini API key error

If the application reports that the Gemini key is missing, verify that ".env" exists and contains:

GEMINI_API_KEY=your_api_key

Restart the application after changing the configuration.

Gemini model unavailable

A Gemini model may become unavailable or inaccessible to a particular API key. In that situation, select another currently supported model in the ".env" configuration.

API quota exceeded

Each comic generation requires multiple Gemini requests. If the API quota is exhausted, wait for the quota to reset or configure another model that is available to your account.

Slow image creation

Stable Diffusion can be very slow when running entirely on a CPU. For quick development tests, use:

IMAGE_PROVIDER=placeholder

A compatible NVIDIA GPU can provide much faster image generation.

GPU memory error

If the GPU runs out of memory, reduce the image resolution or decrease the number of diffusion steps.

Hugging Face access problem

If the model cannot be downloaded, check whether authentication is required and configure the appropriate Hugging Face token.

PDF character problems

The generated PDF uses a standard Latin font. Some special characters, emojis, or unsupported symbols may therefore be replaced or displayed incorrectly.

Project Summary

ComicCraft combines generative AI, image synthesis, web development, and PDF generation into a single application. A user only needs to provide a story concept, and the system automatically develops the narrative, creates comic artwork, arranges the panels, and produces a downloadable comic document.

Team Members

Team Member 1

Name: Tamilarasi S

Degree: BCA

Branch: Computer Application

Year: 2nd Year

Team Member 2

Name: Thanuja j

Degree: BCA

Branch: Computer Application

Year: 2nd Year

Team Member 3

Name: priyanka G

Degree: BCA

Branch: Computer Application

Year: 2nd Year

Team Member 4

Name: jahnavi S

Degree: BCA

Branch: Computer Application

Year: 2nd Year
