# Latte Model Integration with Gradio

This project integrates the **Latte model** from the Diffusers library to generate images from textual prompts using an easy-to-use **Gradio interface**. The Latte model, **Latent Diffusion Transformer**, is designed for advanced video and image generation, providing detailed and high-quality outputs.

## Prerequisites

Make sure you have the following libraries installed before running the project:

```bash
pip install diffusers gradio torch
```

- **Diffusers**: Provides access to pre-trained diffusion models, including the Latte model.
- **Gradio**: Used to create an interactive interface for easy input and output.
- **Torch**: Required for the Latte model to perform computations efficiently.

## How to Use the Gradio Interface

1. **Model Loading**: The Latte model is loaded using the Diffusers library from a pre-trained checkpoint:

   ```python
   from diffusers import DiffusionPipeline

   model_id = "maxin-cn/Latte-1"
   pipe = DiffusionPipeline.from_pretrained(model_id, torch_dtype=torch.float16).to("cuda" if torch.cuda.is_available() else "cpu")
   ```

2. **Interactive Image Generation**: The Gradio interface is designed to allow users to input a caption and generate an image based on that caption:

   ```python
   import gradio as gr

   def generate_image(prompt):
       # Generate an image based on the prompt using the Latte pipeline
       with torch.autocast("cuda"):
           image = pipe(prompt).images[0]
       return image
   
   # Create a Gradio interface
   with gr.Blocks() as demo:
       gr.Markdown("# Generate Images with Latte Model (Latent Diffusion Transformer)")
       
       prompt_input = gr.Textbox(label="Enter Prompt", placeholder="Type a description for your image...")
       generate_button = gr.Button("Generate Image")
       image_output = gr.Image(label="Generated Image")

       generate_button.click(fn=generate_image, inputs=prompt_input, outputs=image_output)

   # Launch the Gradio interface
   demo.launch()
   ```

## Running the Interface

1. **Setup the Environment**: Ensure you have GPU access for efficient generation.
2. **Run the Script**: Execute the above script in Colab, or your local Python setup.
3. **Interactive Use**:
   - A link will be provided to access the Gradio interface.
   - Input a prompt like "Astronaut in a jungle, cold color palette, muted colors" and click on "Generate Image" to get the result.




