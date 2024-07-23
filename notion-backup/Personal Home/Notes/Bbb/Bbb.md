---
Created: 2024-01-17T18:22
URL: https://www.marktechpost.com/2024/01/11/meet-neograd-a-deep-learning-framework-created-from-scratch-using-python-and-numpy-with-automatic-differentiation-capabilities/
---
![[Screenshot-2024-01-08-at-1.57.58-AM.png]]

Understanding how convolutional neural networks (CNNs) operate is essential in deep learning. However, implementing these networks, especially convolutions and gradient calculations, can be challenging. Many popular frameworks like TensorFlow and PyTorch exist, but their complex codebases make it difficult for newcomers to grasp the inner workings.

Meet [neograd,](https://github.com/pranftw/neograd) a newly released deep learning framework developed from scratch using Python and NumPy. This framework aims to simplify the understanding of core concepts in deep learning, such as automatic differentiation, by providing a more intuitive and readable codebase. It addresses the complexity barrier often associated with existing frameworks, making it easier for learners to comprehend how these powerful tools function under the hood.

One key aspect of [neograd](https://neograd.readthedocs.io/en/latest/) is its automatic differentiation capability, a crucial feature for computing gradients in neural networks. This capability allows users to effortlessly compute gradients for a wide array of operations involving vectors of any dimension, offering an accessible means to understand how gradient propagation works.

Moreover, neograd introduces a range of functionalities like gradient checking, enabling users to verify the accuracy of their gradient calculations. This feature helps in debugging models, ensuring that gradients are correctly propagated throughout the network.

The framework also boasts a PyTorch-like API, enhancing users’ familiarity with PyTorch and enabling a smoother transition between the two. It provides tools for creating custom layers, optimizers, and loss functions, offering a high level of customization and flexibility in model design.

Neograd’s versatility extends to its ability to save and load trained models and weights and even set checkpoints during training. These checkpoints help prevent loss of progress by periodically saving model weights, ensuring continuity in case of interruptions like power outages or hardware failures.

Compared to similar projects, neograd distinguishes itself by supporting computations with scalars, vectors, and matrices compatible with NumPy broadcasting. Its emphasis on readability sets it apart from other compact implementations, making the code more understandable. Unlike larger frameworks like PyTorch or TensorFlow, neograd’s pure Python implementation makes it more approachable for beginners, providing a clear understanding of the underlying processes.

In conclusion, neograd emerges as a valuable educational tool in deep learning, offering simplicity, clarity, and ease of understanding for those seeking to comprehend the intricate workings of neural networks. Its user-friendly interface and powerful functionalities pave the way for a more accessible learning experience in deep learning.

Since it enables humans to teach robots any skill, imitation learning via human-provided demonstrations is a promising approach for creating generalist robots. Lane-following in mobile robots, basic pick-and-place manipulation, and more delicate manipulations like spreading pizza sauce or inserting a battery may all be taught to robots through direct behavior cloning. However, rather than merely requiring individual mobility or manipulation behaviors, many activities in realistic, everyday situations need whole-body coordination of mobility and dexterous manipulation.

Research by Standford University investigates whether imitation learning may be used for tasks where bimanual mobile robots need to be controlled with their entire body. Two key issues hamper the widespread use of imitation learning for bimanuaneeds to be improved. (1) Plug-and-play, readily available hardware for whole-body teleoperation needs to be improved. (2) Buying off-the-shelf bimanual mobile manipulators can be expensive. Robots such as the PR2 and the TIAGo are too expensive for typical research labs, costing over USD 200k. More gear and calibration are also required to enable teleoperation on these platforms.

This study addresses the difficulties in implementing imitation learning for bimanual mobile manipulation. Regarding hardware, the researchers introduce Mobile ALOHA, a whole-body teleoperation system that is inexpensive and designed to gather data on bimanual mobile manipulation. By placing it on a wheeled base, Mobile ALOHA expands the possibilities of the original ALOHA, the inexpensive and skillful bimanual puppeteering apparatus.

To permit base movement, the user back drives the wheels while physically attached to the system. This enables the base to move independently while the user controls ALOHA with both hands. They create a whole-body teleoperation system by recording arm puppeteering and base velocity data simultaneously.

The team notes that excellent performance in imitation learning can be obtained by simply concatenating the base and arm actions and then training by direct imitation learning. In particular, they create a 16-dimensional action vector by joining the mobile base’s linear and angular velocity with the 14-DoF joint positions of ALOHA. With nearly no implementation change, this formulation enables Mobile ALOHA to benefit directly from earlier deep imitation learning methods.

They highlight that there are few to no accessible bimanual mobile manipulation datasets. However, they were motivated by the recent success of pre-training and co-training on varied robot datasets to increase imitation learning performance further. As a result, they started using data from static bimanual datasets, which are easier to obtain and more plentiful. In particular, they use the static ALOHA datasets through the introduction of RT-X. It has 825 episodes with activities unrelated to the Mobile ALOHA tasks and has the two arms mounted separately.

Despite the disparities in tasks and morphology, the study demonstrates positive transfer in almost all mobile manipulation tasks, achieving comparable or greater performance and data efficiency than policies taught using only Mobile ALOHA data. Additionally, this observation holds for other classes of cutting-edge imitation learning techniques, such as Diffusion Policy and ACT.

This imitation learning outcome is also robust to many complex activities, including pulling in chairs, contacting an elevator, opening a two-door wall cabinet to store heavy cooking pots, and cleaning up spilled wine. With just 50 human examples for each task, co-training allows us to obtain over 80% performance, with an absolute improvement of 34% on average compared to no co-training.

Check out the [**Paper**](https://mobile-aloha.github.io/resources/mobile-aloha.pdf) and [**Project**](https://mobile-aloha.github.io/). All credit for this research goes to the researchers of this project. Also, don’t forget to follow us on [**Twitter**](https://twitter.com/Marktechpost). Join [**our 35k+ ML SubReddit**](https://pxl.to/8mbuwy)[,](https://pxl.to/8mbuwy) [**41k+ Facebook Community,**](https://www.facebook.com/groups/1294016480653992/) [](https://pxl.to/8mbuwy)[**Discord Channel**](https://pxl.to/8mbuwy), and [**LinkedIn Gr**](https://www.linkedin.com/groups/13668564/)[**oup**](https://www.linkedin.com/groups/13668564/).

[**If you like our work, you will love our newsletter..**](https://marktechpost-newsletter.beehiiv.com/subscribe)