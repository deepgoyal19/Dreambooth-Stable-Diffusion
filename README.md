# Dreambooth-Stable-Diffusion
**                  THIS REPO IS STILL UNDER DEVELOPMENT                         **

**1. ABSTRACT**

The authors of Dreambooth proposed a method to personalize text-to-image
models for generating fully-novel photorealistic images of a subject in
various contexts. Their approach involves fine-tuning a pretrained
text-to-image model with a few reference images to learn a unique
identifier for the subject. By leveraging the semantic prior embedded in
the model and a new autogenous class-specific prior preservation loss,
the technique can synthesize the subject in diverse scenes, poses,
views, and lighting conditions while preserving their key features. In
this report, I will apply the Dreambooth technique to train a diffusion
model on a cat dataset (Fig. 1).

**2. INTRODUCTION**

Dreambooth: Fine Tuning Text-to-Image Diffusion Models for
Subject-Driven Generation is a new approach for "personalizing"
text-to-image models to synthesize photorealistic images of subjects in
different contexts. The method takes a few images of a subject and the
corresponding class name as input and returns a fine-tuned model that
encodes a unique identifier for the subject. At inference time, this
identifier can be used in different sentences to synthesize the subject
in diverse contexts, such as varied scenes, poses, views, and lighting
conditions. This approach has significant implications for fields such
as computer vision, natural language processing, and digital art, as it
addresses the limitations of current large text-to-image models in
accurately mimicking the appearance of subjects and synthesizing new
renditions in different contexts.

**3. DATASET**

The dataset comprises eight images of a British Shorthair cat, each with
a resolution of 1080 pixels by 1080 pixels.

![](media/image1.jpeg){width="6.25in" height="0.7819444444444444in"}

**Fig. 1.** Shows the images from the cat dataset.

**4. EXPERIMENTS**

To fit the Dreambooth model perfectly on the training dataset, several
experiments were conducted by adjusting the learning rate, parameters,
and stable diffusion models. These experiments were performed at a
resolution of 512x512.

**4.1 Terminologies:**

-   **Unique class**: Examples include "dog", "person", etc. In this
    example, we use "cat".

-   **Unique identifier**: A unique identifier that is prepended to the
    unique class while forming the "instance prompts". In this example,
    we use "sks" as this unique identifier.

-   **Instance prompt**: Denotes a prompt that best describes the
    "instance images". An example prompt could be - "a photo of
    {unique\_id} {unique\_class}". So, for our example, this becomes -
    "a photo of sks cat".

-   **Class prompt**: Denotes a prompt without the unique identifier.
    This prompt is used for training data with prior preservation. For
    our example, this prompt is - "a photo of cat".

-   **Instance images**: Denote the images that represent the visual
    concept you're trying to teach aka the "instance prompt". This
    number is typically just 3 - 5. We typically gather these
    images ourselves.

-   **Class images**: Denote the images generated using the "class
    prompt" for using prior preservation in Dreambooth training. We
    leverage the pre-trained model before fine-tuning it to generate
    these class images.

-   **Class images prompt**- Denotes a prompt without the
    unique identifier. This prompt is used for generating "class images"
    for prior preservation. For our example, this prompt is - "a photo
    of golden british shorthair cat".

-   **Text Encoder Steps**- Denotes the number of training steps
    executed using a text encoder to fine-tune the model subsequent to
    training without a text encoder. For our example, the training
    lasted for 1600 steps without a text encoder, and then an additional
    200 steps were performed with a text encoder to fine-tune the model.

**4.2 Experiment 1**

The outcomes, as presented in Table 1, were discovered to be the poorest
performing. Despite conducting an extra 200 steps using a text encoder
to avert overfitting, it failed to yield satisfactory results.

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **TABLE 1**
  -------------------------------------------- ------------------------------------------------------- -------------------- ------------------------ ------------------------------------------------------------------------------------
  **Model Info**

  **Instance Prompt-**

  a photo of a &lt;sks&gt; cat

  **Class Prompt-**

  a photo of a golden british short hair cat

  **Class Images prompt -**

  a photo of a golden british short hair cat

  **Instance Prompt-**

  a photo of a &lt;sks&gt; cat

  **Class Prompt-**

  a photo of a cat

  **Class Images prompt-**

  a photo of a golden british short hair cat

  **Instance Prompt-**

  a photo of a &lt;sks&gt; cat

  **Class Prompt-**

  a photo of a cat

  **Class Images prompt -**

  A photo of a cat

  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**4.3) EXPERMENT 2**

The model trained for 1600 training steps w/o text encoder had been
found the perfect fit as shown in Table 2.

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **TABLE 2**
  -------------------------------------------------------------------- ------------------------------------------------------------------------------------------------- --------------------------------------------------- -------------------- ------------------ -------------------------------------------------------------------------------------
  **Model Info**

  **Class prompt**- a photo of cat

  **Instance Prompt-** a photo of &lt;sks&gt; cat

  **Class Images prompt -** a photo of golden British short hair cat

  **Pretrained Model Name-** Stable-diffusion-v1-5

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**4.4) EXPERMENT 3**

Once the ideal number of training steps was identified, the author
proceeded to train the model using distinct class prompts and class
image prompts. However, this model did not fit well as the cat's eyes
were not accurately depicted in the images as shown in Table 3.

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **TABLE 3**
  ----------------------------------------------------------------------------------------------------------------- ----------------------------------------------------- -------------------- -------------------------------------------------------------------------------------
  **Model Info**

  **Class prompt-** a photo of golden British short hair cat

  **Instance Prompt-** a photo of &lt;sks&gt; cat

  **Class Images prompt -** a photo of golden British short hair cat

  **Pretrained Model Name-**

  Stable-diffusion-v1-5

  **Model Link-** [Link](https://drive.google.com/drive/folders/1uTLNE3bCFUsAoX9KPzx3QSV6ZueTM947?usp=share_link)

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**4.5) EXPERMENT 4**

the author proceeded to train the model using distinct class prompts and
class image prompts. However, this model did not fit well due to
overfitting as shown in Table 4.

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **TABLE 4**
  ----------------------------------------------------------------------------------------------------------------- ----------------------------------------------------- -------------------- ----------------------------------------------------------------------
  **Model Info**

  **Class prompt-** a photo of cat

  **Instance Prompt**- a photo of &lt;sks&gt; cat

  **Class Images prompt -** a photo of cat

  **Model Link-** [Link](https://drive.google.com/drive/folders/1gaeDZ3ynIb_hTKr2dqaepP8yTEE2n8Hp?usp=share_link)

  **Pretrained Model Name-** Stable-diffusion-v1-5

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**4.6) EXPERMENT 5**

From the above experiments it was concluded that class image prompt “a
photo of golden British short hair cat “. In this experiment author
tested the same number of training steps on the other stable diffusion
model (Stable-diffusion-v1-4). However, this model did fit perfect well
but not as perfect as the model with 1600 training steps w/o text
encoder as shown in table 2 and table 7.

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **TABLE 5**
  -------------------------------------------------------------------- ----------------------------------------------------- -------------------- -------------------------------------------------------------------------------------
  **Model Info**

  **Class prompt-** a photo of cat

  **Instance Prompt-** a photo of &lt;sks&gt; cat

  **Class Images prompt -** a photo of golden British short hair cat

  **Pretrained Model Name-**

  Stable-diffusion-v1-4

  **Model Link-** Link

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**4.7) EXPERMENT 6**

The model did not perform well and produced the poorest outcomes among
all the experiments as shown in table 6.

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **TABLE 6**
  ----------------------------------------------------------------------------------------------------------------- ----------------------------------------------------- -------------------- -------------------------------------------------------------------------------------
  **Model Info**

  **Class prompt-** a photo of cat

  **Instance Prompt-** a photo of &lt;sks&gt; cat

  **Class Images prompt -** a photo of golden British short hair cat

  **Pretrained Model Name-** Stable-diffusion-2

  **Model Link-** [Link](https://drive.google.com/drive/folders/1RChDJK-wGrTjmNl-DJFaR2sQQDUt0pfh?usp=share_link)

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**5. RESULTS AND ANALYSIS**

**5.1) RESULT OUPUT**

The model has achieved a perfect fit using stable diffusion-v1-5 and the
class image prompt "a photo of a golden British short hair cat" as shown
in table 7.

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **TABLE 7**
  ------------------------------------------------------------------------------------------------------------------ --------------------------------------------------------- -------------------------------------------------------------------------------------
  **Model Info**

  **Class prompt**- a photo of cat

  **Instance Prompt-** a photo of &lt;sks&gt; cat

  **Class Images prompt-** a photo of golden British short hair cat

  **Pretrained Model Name-** Stable-diffusion-v1-5

  **Model Link-** [Link](https://drive.google.com/drive/folders/1tjSIgjwb0_8kVttWwXRaoFSHwQWEynaj?usp=share_link)

  **Result Link-** [Link](https://drive.google.com/drive/folders/1uNKxoC30jk39By4uBGBOr6pl0Zix_TTv?usp=share_link)

  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**5.2) CODE SNIPPET**

To produce the optimal outcomes, some of the code's hyperparameters and
components were adjusted. This code was obtained from Hugging Face's
official GitHub
repository.![](media/image27.PNG){width="5.715277777777778in"
height="3.0069444444444446in"}

**Fig. 2.** shows the code snippet of the model.

[Google Colab
Link](https://colab.research.google.com/drive/1kScSRsJJ5ZNPbcm4FdGTs7IjcXYX1a_u?usp=share_link)

**5.3) ANALYSIS**

**Learning Rate**

-   During testing, a learning rate of 1e-6 consistently produced good
    results across all experiments.

-   However, it was observed that increasing the learning rate beyond
    1e-6 resulted in overfitting of the model.

**Prompts**

-   Both the class prompt and the prompt used to generate class images
    were found to have a noticeable impact on the model's output.

-   The impact of class prompts on training was found to be relatively
    minor compared to the effect of generated class images. Therefore,
    it is recommended to use class images that closely resemble the
    subjects in the training dataset. It is also suggested that class
    prompts should not be specified for the training data. For instance,
    a class prompt such as "a photo of cat" is preferable over a more
    specific class prompt like "a photo of golden British short
    hair cat".

-   The model was found to have a high level of accuracy when tested
    with class images generated by the prompt "a photo of golden British
    short hair cat" and a class prompt of "a photo of cat," as these
    images closely resembled the subjects in the training dataset. This
    resulted in the model demonstrating a perfect fit for the project.

**Prior preservation**

-   In the initial tests model tends to overfit without
    prior preservation. So, all the results have been performed with
    prior preservation.

**Stable Diffusion Model**

-   Among the different models tested, Stable Diffusion v1-5 was found
    to have the best performance.

-   Stable Diffusion v1-4 was observed to perform better than Stable
    Diffusion v2, but not as well as Stable Diffusion v1-5.

-   Our training dataset showed the worst performance with Stable
    Diffusion v2 when compared to the other models tested.

**Text encoder**

-   The process of fine tuning the encoder from the initial training
    stages led to overfitting.

-   the model was trained for a few hundred steps by fine tuning the
    encoder after training for thousands of steps, which resulted in the
    production of distorted images.

-   Better outcomes were achieved by freezing the text encoder.

**Noise Scheduler**

-   The DDIM scheduler proved to be a good fit for our training dataset.

**-----------------------------------------------------------END----------------------------------------------------------**
