---
Created: 2024-02-18T10:40
URL: https://towardsdatascience.com/an-introduction-to-fine-tuning-pre-trained-transformers-models-9ea546611664
---
# An Introduction To Fine-Tuning Pre-Trained Transformers Models

## Simplified utilizing the HuggingFace trainer object

[![](https://miro.medium.com/v2/resize:fill:88:88/1*brMlNn0wRUT0G19S3L-QPQ@2x.jpeg)](https://miro.medium.com/v2/resize:fill:88:88/1*brMlNn0wRUT0G19S3L-QPQ@2x.jpeg)

[![](https://miro.medium.com/v2/resize:fill:48:48/1*CJe3891yB1A1mzMdqemkdg.jpeg)](https://miro.medium.com/v2/resize:fill:48:48/1*CJe3891yB1A1mzMdqemkdg.jpeg)

[Ram Vegiraju](https://ram-vegiraju.medium.com/?source=post_page-----9ea546611664--------------------------------)

·

[Follow](https://medium.com/m/signin?actionUrl=https%3A%2F%2Fmedium.com%2F_%2Fsubscribe%2Fuser%2F6e49569edd2b&operation=register&redirect=https%3A%2F%2Ftowardsdatascience.com%2Fan-introduction-to-fine-tuning-pre-trained-transformers-models-9ea546611664&user=Ram+Vegiraju&userId=6e49569edd2b&source=post_page-6e49569edd2b----9ea546611664---------------------post_header-----------)

Published in

[Towards Data Science](https://towardsdatascience.com/?source=post_page-----9ea546611664--------------------------------)

·

5 min read

·

1 day ago

Image from [Unsplash](https://unsplash.com/photos/matrix-movie-still-iar-afB0QQw) by [Markus Spiske](https://unsplash.com/@markusspiske)

[![](https://miro.medium.com/v2/resize:fit:700/0*GD1Mk7qF1YLrqDMQ)](https://miro.medium.com/v2/resize:fit:700/0*GD1Mk7qF1YLrqDMQ)

[HuggingFace](https://huggingface.co/) serves as a home to many popular open-source NLP models. Many of these models are effective as is, but often require some sort of training or fine-tuning to improve performance for your specific use-case. As the LLM implosion continues, we will take a step back in this article to revisit some of the core building blocks HuggingFace provides that simplify the training of NLP models.

Traditionally NLP models can be trained using vanilla PyTorch, TensorFlow/Keras, and other popular ML frameworks. While you can go this route, it does require a deeper understanding of the framework you are utilizing as well as more code to write the training loop. With HuggingFace’s [Trainer class](https://huggingface.co/docs/transformers/main_classes/trainer), there’s a simpler way to interact with the NLP Transformers models that you want to utilize.

Trainer is a class specifically optimized for [Transformers](https://github.com/huggingface/transformers) models and also provides tight integration with other Transformers libraries such as [Datasets](https://huggingface.co/docs/datasets/en/index) and [Evaluate](https://huggingface.co/docs/evaluate/en/index). Trainer at a more advanced level also supports distributed training libraries and can be easily integrated with infrastructure platforms such as Amazon SageMaker.

In this example we’ll take a look at using the Trainer class locally to fine-tune the popular BERT model on the [IMBD dataset](https://huggingface.co/datasets/imdb) for a Text Classification use-case([Large Movie Reviews Dataset](https://ai.stanford.edu/~amaas/data/sentiment/) [Citation](https://ai.stanford.edu/~amaas/papers/wvSent_acl2011.bib)).

**NOTE**: This article assumes basic knowledge of Python and the domain of NLP. We will not get into any specific Machine Learning theory around model building or selection, this article is dedicated to understanding how we can fine-tune the existing pre-trained models available in the HuggingFace Model Hub.

# Table of Contents

1. Setup
2. Fine-Tuning BERT
3. Additional Resources & Conclusion

# 1. Setup

For this example, we’ll be working in [SageMaker Studio](https://aws.amazon.com/sagemaker/studio/) and utilize a conda_python3 kernel on a ml.g4dn.12xlarge instance. Note that you can use a smaller instance type, but this might impact the training speed depending on the number of CPUs/workers that are available.