New and Modern Techniques & Subfields

[NLP] 
- Natural Language Processing
	- human language processing
	- Summarization, Chatbots, Generative M.L. Models
- lead to self-supervised learning
	- [hybrid] unsupervised + supervised Learning
	- which lead to Language Models, then
	- Large Language Models
		- predict missing word through context of previous words
		- synthesizes human language/speech patters

LLMs are example of Deep Learning
- most recent llm architecutre [revolutionary~2017]: transformers
- transformers process text by selectively focusing on relevant parts of the sequence at each step
	- done through an [Attention Mechanism]
	- the Self Attention Mechanism employed: Self-Attention
		- calculates significance of various words or other tokens in input seq. to generate an output
		- i.e., Big red dog.
			- big applies to dog more than red 
			- red applies to dog more than big
			- and dog applies to neither; independent
	- GPT = Generative Pre-trained Transformer
		- generative = makes an output; prediction
		- pre-trained = pre-trained on a data set
		- transformer = neural network architecture

Diffusion = 
- mostly images creation
Generative Adversarial Network = [GANs]
- unique because has two outputs
	- one output for *image, text* 
	- another output for judgment of output quality
Neural Radiance Fields = [NRFs]
- 3d Modeling
Hybrid Models =
- any combo of the above

M.L. Use Cases
Fradualent Banking
- train on user data with the scores evaluated on prediction of fraudulent activities from that user
Client Retention
- can be automated, identify unknown trends