# wgt-talk

Links:
* Olga Kahn on recent experience as a Data Scientist [link](http://olgakahn.com/projects/recap)
* Peter Baumgartner on Ways I Use Testing as a Data Scientist [link](https://www.peterbaumgartner.com/blog/testing-for-data-science/)
* David Robinson on Scientific Debt [link](http://varianceexplained.org/r/scientific-debt/)
* Zachary Lipton on The Deception of Supervised Learning [link](https://www.approximatelycorrect.com/2017/02/14/the-deception-of-supervised-learning-v2/)
* Sean Taylor on Designing and Evaluating metrics [link](https://medium.com/@seanjtaylor/designing-and-evaluating-metrics-5902ad6873bf)
* Zachary Thomas on The Definitive Guide to Designing Product Metrics [link](https://towardsdatascience.com/the-definitive-guide-to-designing-product-metrics-ba5d9e8e07e9)
* Emmanuel Ameisen on Always start with a stupid model, no exceptions [link](https://blog.insightdatascience.com/always-start-with-a-stupid-model-no-exceptions-3a22314b9aaa)

Books:
* Christian, Brian, and Tom Griffiths. Algorithms to live by: The computer science of human decisions. Macmillan, 2016.
* Thinking with Data by Max Shron
* Kohavi, Ron, Diane Tang, and Ya Xu. Trustworthy online controlled experiments: A practical guide to a/b testing. Cambridge University Press, 2020

Papers:
* Sculley, David, et al. "Hidden technical debt in machine learning systems." Advances in neural information processing systems 28 (2015): 2503-2511. [pdf](https://proceedings.neurips.cc/paper/2015/file/86df7dcfd896fcaf2674f757a2463eba-Paper.pdf)
* Bernardi, Lucas, Themistoklis Mavridis, and Pablo Estevez. "150 successful machine learning models: 6 lessons learned at booking. com." Proceedings of the 25th ACM SIGKDD International Conference on Knowledge Discovery & Data Mining. 2019. [pdf](https://blog.kevinhu.me/2021/04/25/25-Paper-Reading-Booking.com-Experiences/bernardi2019.pdf)
* Ye, Peng, et al. "Customized regression model for airbnb dynamic pricing." Proceedings of the 24th ACM SIGKDD international conference on knowledge discovery & data mining. 2018. [pdf](https://dl.acm.org/doi/10.1145/3219819.3219830)
* Huang, Shan, Michael Allan Ribers, and Hannes Ullrich. "Assessing the value of data for prediction policies: The case of antibiotic prescribing." Economics Letters 213 (2022): 110360.[pdf](https://www.sciencedirect.com/science/article/pii/S0165176522000490?via%3Dihub)
* Smith, Adam N., Stephan Seiler, and Ishant Aggarwal. "Optimal Price Targeting." Available at SSRN 3975957 (2021). [pdf](https://papers.ssrn.com/sol3/papers.cfm?abstract_id=3822459)
* Yang, Jeremy, et al. "Targeting for long-term outcomes." arXiv preprint arXiv:2010.15835 (2020). [pdf](https://arxiv.org/abs/2010.15835)

Courses:
* Causal Diagrams: Draw Your Assumptions Before Your Conclusions [webpage](https://www.edx.org/course/causal-diagrams-draw-your-assumptions-before-your)

**Questions to ask:**
1. Describe the user/system story?
* How decisions are made without a model currently? 
* How embedding a model inside/instead of existing workflow is going to change it? 
* How specifically model outputs are going to be used? As Kleinberg et al. (2017) in [“Human decisions and machine predictions”](https://academic.oup.com/qje/article-abstract/133/1/237/4095198?redirectedFrom=fulltext) have shown “being clear about how predictions translate to decisions can substantially influence how the prediction function is evaluated”.  
* Note that business problems such as pricing, inventory management, or marketing allocation that are typically addressed with prediction models, require more robust causal assumptions to guide optimal decision outcomes (see Bertsimas et al. (2016) [The Power and Limits of Predictive Approaches to Observational-Data-Driven Optimization](https://arxiv.org/abs/1605.02347))

2. Describe the data generating process
* Formalise the knowledge about the steps above. 
* What is the [Directed Acyclic Graph](https://en.wikipedia.org/wiki/Directed_acyclic_graph) (DAG) that generates the data? DAG helps to build causally valid models, useful for decision-makers - see the following [article](https://towardsdatascience.com/be-careful-when-interpreting-predictive-models-in-search-of-causal-insights-e68626e664b6) as an example. Clear guidance how to build DAG (or causal diagrams) and how to use them to build causal model is provided in [Behavioral Data Analysis with R and Python](https://learning.oreilly.com/library/view/behavioral-data-analysis/9781492061366/).
* Where is the model going to be placed? See search query click-through prediction example in Figure 3 in Bottou et al. “[Counterfactual Reasoning and Learning Systems: The Example of Computational Advertising](https://www.microsoft.com/en-us/research/wp-content/uploads/2013/11/bottou13a.pdf)”. 
* What are the [nuisance](https://en.wikipedia.org/wiki/Nuisance_parameter#:~:text=In%20statistics%2C%20a%20nuisance%20parameter,%CE%BC%2C%20is%20of%20primary%20interest.) parameters?
* What are the [degrees of freedom](https://en.wikipedia.org/wiki/Degrees_of_freedom) in the results of off-line and on-line validation?

3. State a single hypothesis that will be tested in your project
* Even something as simple as “There is a supervised signal in user-generated features to predict churn above a baseline” is sufficient for the start. One can iterate on hypotheses. 

4. Describe a clear off-line validation method & metric
* Here we should not be afraid to dedicate more time on developing an appropriate off-line validation method and the metrics that are as close as possible to what actually matters at deployment (see [Designing and Evaluating metrics](https://medium.com/@seanjtaylor/designing-and-evaluating-metrics-5902ad6873bf) or [Off-policy metrics](https://edoconti.medium.com/offline-policy-evaluation-run-fewer-better-a-b-tests-60ce8f93fa15)). 
* E.g. If our model is going to be predicting over-time then validation should include time aspect when needed (time-nested cross validation). 
* Does the model interact with the environment - if so the offline validation method should do its best to account for it (see Z. Lipton on “[The deception of supervised learning](http://approximatelycorrect.com/2017/02/14/the-deception-of-supervised-learning-v2/)”) 
* Our off-line metric should be as close as possible to the online metric we care for, e.g. if we are developing a price model we could take inspiration from  Ye et al. “Customized Regression Model for Airbnb Dynamic Pricing”. 

5. State the baseline that will be used during off-line validation
* There should always be a simple baseline to compare the model against. See “[Always start with a stupid model, no exceptions](https://blog.insightdatascience.com/always-start-with-a-stupid-model-no-exceptions-3a22314b9aaa)” for more details. Use that baseline to evaluate a complete off-line validation setup, and in some cases perform even an online validation. It is useful to use [The Heuristic Benchmark pattern](https://learning.oreilly.com/library/view/machine-learning-design/9781098115777/ch07.html#design_pattern_twoeight_heuristic_bench) that compares an ML model against a simple, easy-to-understand heuristic in order to explain the model’s performance to business decision makers.

6. Describe the online validation method for the hypothesis
* We should in advance dedicate time to outline the AB test within which the model is going to be tested. 
* Are there processes that may interfere with the experiment outcome? Answering the questions alike can help design a better off-line validation method.  
