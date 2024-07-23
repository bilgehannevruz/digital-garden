---
Created: 2024-03-10T09:57
URL: https://towardsdatascience.com/a-guide-to-data-pipeline-testing-with-python-a85e3d37d361
---
# A Guide To Data Pipeline Testing with Python

## A gentle introduction to unit testing, mocking and patching for beginners

[![](https://miro.medium.com/v2/resize:fill:88:88/1*y_diTp0WnTe2m4Nevkfjtw.png)](https://miro.medium.com/v2/resize:fill:88:88/1*y_diTp0WnTe2m4Nevkfjtw.png)

[![](https://miro.medium.com/v2/resize:fill:48:48/1*CJe3891yB1A1mzMdqemkdg.jpeg)](https://miro.medium.com/v2/resize:fill:48:48/1*CJe3891yB1A1mzMdqemkdg.jpeg)

[💡Mike Shakhomirov](https://mshakhomirov.medium.com/?source=post_page-----a85e3d37d361--------------------------------)

·

[Follow](https://medium.com/m/signin?actionUrl=https%3A%2F%2Fmedium.com%2F_%2Fsubscribe%2Fuser%2Fe06a48b3dd48&operation=register&redirect=https%3A%2F%2Ftowardsdatascience.com%2Fa-guide-to-data-pipeline-testing-with-python-a85e3d37d361&user=%F0%9F%92%A1Mike+Shakhomirov&userId=e06a48b3dd48&source=post_page-e06a48b3dd48----a85e3d37d361---------------------post_header-----------)

Published in

[Towards Data Science](https://towardsdatascience.com/?source=post_page-----a85e3d37d361--------------------------------)

·

9 min read

·

14 hours ago

AI-generated image using [Kandinsky](https://github.com/ai-forever/Kandinsky-2)

[![](https://miro.medium.com/v2/resize:fit:700/1*vR37NXcWxA9XFtNFZxyi3w.png)](https://miro.medium.com/v2/resize:fit:700/1*vR37NXcWxA9XFtNFZxyi3w.png)

In this story, I would like to raise a discussion about unit testing in data engineering. Although there are plenty of articles on Python unit testing on the internet, the topic looks a bit vague and uncovered. We will speak about data pipelines, the parts they consist of and how we can test them to ensure continuous delivery. Each step of the data pipeline can be considered as a function or process and ideally, it should be tested not only as a unit but all together, integrated into one single data flow process. I’ll try to summarize the techniques that I use often to mock, patch and test data pipelines including integration and automated tests.

## What is unit testing in the data world?

Testing is a crucial part of any software development lifecycle and helps developers make sure the code is reliable and can be easily maintained in the future. Consider our data pipeline as a set of processing steps or functions. In this case, unit testing can be considered as a technique of writing tests to ensure that each unit of our code, or each step of our data pipeline doesn’t produce unintended results and is fit for purpose.

> In a nutshell, each step of a data pipeline is a method or function which needs to be tested.

Data pipelines might be different. In fact, they often vary greatly in terms of data sources, processing steps and final destinations for our data. Whenever we transform the data from point A to point B, there is a data pipeline. There are different design patterns [1] and techniques to build these data processing graphs and I wrote about it in one of my previous articles.

## [Data pipeline design patterns](https://towardsdatascience.com/data-pipeline-design-patterns-100afa4b93e3?source=post_page-----a85e3d37d361--------------------------------)

### [Choosing the right architecture with examples](https://towardsdatascience.com/data-pipeline-design-patterns-100afa4b93e3?source=post_page-----a85e3d37d361--------------------------------)

[towardsdatascience.com](https://towardsdatascience.com/data-pipeline-design-patterns-100afa4b93e3?source=post_page-----a85e3d37d361--------------------------------)

Take a look at this simple data pipeline example below. It demonstrates a common use case scenario when data is being processed in the multi-cloud. Our data pipeline starts from the…