 

RISK-AWARE RECOMMENDER
FOR E-COMMERCE
by


Nguyen Trong Quoc Dat
Nguyen Nhat Minh
Tran Le Anh Tuan






FPT UNIVERSITY




RISK-AWARE RECOMMENDER
FOR E- COMMERCE

by
Nguyen Trong Quoc Dat
Nguyen Nhat Minh
Tran Le Anh Tuan
Supervisor: Master. Phan Thanh Huy
DEPARTMENT OF ITS
FPT UNIVERSITY



A final year capstone project submitted in partial fulfillment of the requirement
for the Degree of Bachelor of Artificial Intelligence in Computer Science


April 2024




ACKNOWLEDGMENTS
With great respect, we would like to express our sincere gratitude to those who helped us to be able to complete this capstone project. We extend our deepest and most sincere gratitude to our advisor, Master Phan Thanh Huy, for always supporting us, giving us great advice and keeping this project on track.

Thanks to the teacher for taking the time to review our project and give us some really helpful feedback. Seriously, those comments helped us a lot in completing this project and we are very grateful for the insights you shared with us.

I truly appreciate my colleagues and friends at the FPT University for cheering us on and helping us when we needed it. Your support and willingness to share your knowledge were invaluable in contributing to the completion of this project.

Last but not least, this project could not have been completed without the help of the individuals above. Once again, we thank you from the bottom of our hearts for all your help and support throughout the project.


 


ABSTRACT
Nowadays, Recommender systems have played a crucial role in our daily lives. With the explosion of online shopping, also known as e-commerce, it is challenging for common recommendation tricks to work without much history of new users or items. For that reason, we have been digging deeper into this problem, testing new ways to make recommendation systems smarter even when they have little past data. We used several machine learning models to directly address this challenge. Hopefully, our work will advance personalized recommendations in the ever-changing world of online shopping.
 
In our project, we used several methods such as re-ranking, in addition to combining with base models such as CLCRec and CCFCRec to apply to this problem for training, testing and compare accuracy with existing base models but do not focus on cold-start phase. We will clarify each one in the following sections.
Keywords: Risk Awareness; Cold-start; Recommender system; CLCRec, CCFCRec.
 
CONTENTS
ACKNOWLEDGMENTS	3

ABSTRACT	4

CONTENTS	5

List of Figures	7

List of Tables	8

1. INTRODUCTION	9
	1.1 Overview	9
		1.1.1 Overview Of Risk-Awareness	13 
		1.1.2 Fairness Context	13
		1.1.2 Cold-start Context	13
	1.2 Fairness Issues During The Cold-start Phase	14
	1.2 Re-ranking 	14
	1.2 Our works	15

2. RELATED WORK	16

	2.1 Fairness Definitions In Recommendation	16

	2.2 Re-ranking method	17

	2.3 Base model	18

2.3.1 CLCRec	18

2.3.2 CCFCRec	20

2.3.2.1 Problem Fomulation	21

2.3.2.2 CCFCRec Architectures	22

	2.4 Metrics	24

2.4.1 Precision@K	24

2.4.2 Recall@K	25

2.4.2 NDCG@K	25

2.4.2 MDG	26

3. PROJECT MANAGEMENT PLAN	27

4. MATERIALS AND METHODS	32

5. RESULTS	36

6. DISCUSSIONS	38

7. DEPLOYMENT	39

8. CONCLUSIONS	43

9. APPENDIX A	45

10. APPENDIX B	46 

11. APPENDIX C	47 

12. REFERENCES	49
 

List of Figures
1.1 Figure 1. Illustrations the content-based filtering	10
1.1 Figure 2. Illustrations the collaborative filtering	11
1.1 Figure 3. Illustrations the hybird recommendation	12
2.2 Figure 4. Illustrations for different re-ranking types	17
2.3 Figure 5. Illustrations architecture of base model CLCRec	18
2.3 Figure 6. Illustrations architecture of base model CCFCRec	22
7.4 Figure 7. Homepage of our E-commerce website	40
7.4 Figure 8. Recommendation page	41
7.4 Figure 9. Interaction history page	42































List of Tables
3   Table 3.1  Weekly Project Plan	29
3   Table 3.1  Weekly Task Assignment	30
5   Table 5.1  Comparation	36
Appendix Table B.1. Source 	47
Appendix Table C.1. Errors during import of base model	48






 

 





Chapter 1

INTRODUCTION



1.1 Overview

In the realm of customized electronic products, recommender systems are crucial for enhancing user experiences and assisting in finding appropriate products. They are utilized across various industries such as e-commerce, healthcare, education, etc. Users usually tends to stay on your website for a longer duration when your recommender system recommends a film they are likely to enjoy. The longer they stay, the more advertisements can be shown to them, resulting in increased revenue from advertising. In the current landscape, many retail stores have shut down some physical locations and transitioned to e-commerce as a fresh approach to promote and sell their products and services. 
The e-commerce recommendation system works by suggesting items according to the user's preferences and interests. There are numerous approaches to pique a user's interest, and every recommendation system will identify it in a unique way. Recommendation systems can gather user preferences or interests through three primary ways: content-based filtering approach, collaborative filtering approach, and hybird approach. Additionally, methods like demographic, knowledge-based, and community-based approaches exist, but we will only focus on the three most common types.







Content-based Filtering. Content-based filtering approach suggests items based on the user's profile or based on the content/attributes of items similar to items the user has selected in the past. Show in Fig.1.





 

Fig. 1. Illustrations the content-based filtering





















Collaborative Filtering. Collaborative filtering approach suggests items based on similarity between users or items. Simply explained, this is a way to suggest a user based on the behavior of similar users. Collaborative filtering can be done in two ways: the first is user-based collaborative filtering, which finds users who are most similar to one another and shares their preferences with other users [1]. Item-based collaborative filtering, which is based on items and suggests related items that are appreciated by several users [2, 3], is the second kind. Show in Fig.2.




 

Fig. 2. Illustrations the collaborative filtering
Hybrid Recommendation. Hybrid approach is a method that combines the techniques mentioned above. For example, the CF method will have problems with new items, meaning it cannot provide suggestions for unrated items. However, this does not affect content-based because this method predicts items based on their descriptions. Combining these two methods can help the system take advantage of one technique to complement the other.




 

Fig. 3. Illustrations the hybird recommendation


In addition, there are two very interesting aspects of the recommender system: risk awareness and cold-start problem. We will go into further detail about these two factors below.












1.1.1 Overview Of Risk-Awareness

Recommendation systems today employ product introduction to draw in customers by taking into account factors like not upsetting users in particular situations or during particular times of the day. The following scenarios could happen: age, gender, race, time, context, etc. Therefore, the level of risk directly impacts the performance of the system. These systems leverage advanced algorithms and user behavior analytics to provide relevant and personalized product recommendations for each shopper. With the huge amount of data generated by online transactions, browsing history, and user preferences, recommendation systems play a vital role in enhancing the overall shopping experience. By understanding each customer's unique needs and preferences, e-commerce platforms can not only increase customer satisfaction but also drive engagement and increase sales.
Risk definition: “Risk is disturbing or annoying the user, which can directly cause adverse effects on system performance.” [4].  


1.1.2 Fairness Context

But are the recommended items fair? For example, in an online shopping product (item) recommendation engine that offers shopping suggestions to users, but whether users with different attributes such as gender, race, age, etc. are treated equally? In the morning news, are different political stories presented fairly against each other? And are products from big companies popular with new users? Potential problems and suggestions are noted in the documents [5, 6, 7, 8, 9] with potential negative impacts on suppliers of those goods.


1.1.3 Cold-start Context

In most real-world applications, making recommendations on new items without any historical interaction from the user (formally known as cold start recommendation tasks), this is a challenge that has long existed in recommender systems. That is, how to onboard new users and new items without any historical interaction? ML methods often incorporate both user interaction data and existing cold boots (e.g. collaborative filtering methods). However, these approaches face many disadvantages such as the long distance from the conversion functions to the model's output layer, in addition to the consistency problem when applying the same conversion function to users. and various entries lead to poor transformations that produce poor model output (increasing the final recommendation error). Dive into the cold start problem that occurs when the system does not have any relationship between the user and the items for which the system does not have enough data. There are two types of cold start:
1. User cold-start problems: When the system does not have any information about the user, it means the user has just registered and has not had any interaction with the system, so the system cannot provide personalized suggestions.
2. Item cold-start problems: When there is almost no information about the item, it may be because the item has just been added, or the item already has some content information but no user interaction.

1.2 Fairness Issues During The Cold-start Phase

Addressing equity in the context of cold starts is imperative to ensure fair, enhanced user experiences and prevent the propagation of false biases. Achieving fairness in early recommender systems requires a delicate balance of incorporating diverse user preferences without perpetuating existing biases from historical data. In addition, sensitive user information must also be secured. This report explores the different methods used to improve fairness in cold start situations, including Separate-training methods [10, 11, 12, 13, 14] and joint-training methods [15, 16, 17]. By closely examining the fairness aspects of recommendation systems in e-commerce, this report aims to contribute to the development of more comprehensive and objective recommendation mechanisms that promote trust and user satisfaction across diverse and growing online markets. However, there is no concept of fairness in cold start systems. Specifically, in this article we will use three cold start recommendation systems CCFCRec [18], and CLCRec [19] to solve the fairness problem.


1.3 Re-ranking 

The pursuit of optimizing recommender systems for e-commerce, by incorporating ranking methods, represents a strategic development in enhancing the effectiveness of existing techniques to address fairness in cold start situations. Re-ranking introduces a layer of post-processing that refines initial recommendations by considering additional dimensions such as user preferences, item characteristics, and fairness metrics. The combination of reordering with these start-from-scratch strategies gives greater adaptability to recommender systems, allowing them to dynamically adapt and fine-tune recommendations to relevant users with limited historical work. By integrating a re-ranking strategy, the recommendation system not only aligns with fairness goals but also personalized recommendations based on the user, tailoring them to individual user profile score. This report delves into the key role of rerating as a complementary technique to cold start problems, explores the synergies between these methods, and sheds light on their joint impact on fairness and user satisfaction in the field of e-commerce.






1.4 Our Works

In this article we are interested in two issues: cold start item for recommender system, and solving the issue of fairness in risk awareness using the reranking method. Our wish is to be able to handle the cold start problem of the recommender system while increasing the fairness of the system for users, specifically group fairness, without affecting the performance of the system. We will delve into the details of e-commerce recommendation systems and explore fresh ways to make them more accurate, fair, and personalized, especially when starting from scratch. We are all about shaking things up by combining and upgrading models that already exist to fine-tune those initial suggestions. We will mix some theory on the tricky cold start problem and fairness for users with real-world examples from big players like Amazon. By doing this, we will see how combining cold start strategies with realignment methods can boost recommendation accuracy and maybe even make online shopping more inclusive, adaptable, and satisfying for everyone.



































Chapter 2

RELATED WORK



2.1 Fairness Definitions In Recommendation

The recommendation system plays an important role in distributing information by providing personalized recommendations to users based on their interests or behaviors so that users can easily come into contact with items. Regarding distribution, there are two aspects that deserve attention. The first is the fair item allocation process, such as the fairness of the recommendation model. The second is the distributional outcome, such as the fairness of the information that users will receive. But in our article, we will only cover grouping by target. Grouped by Target. Based on whether the goal is to ensure fairness at individual-level or the group-level, fairness of outcomes can be classified into individual fairness and group fairness:
Group Fairness. In-group fairness dictates that protected groups should be treated similarly to advantaged groups as a result, which means that groups should be treated differently across the board. We can divide groups into many different ways, the most common is based on some obvious attributes related to some sensitive attributes such as gender, race, age, etc. In addition, when in groups with many related sensitive attributes, we can divide the groups into smaller groups. However, we still have to consider the fairness of these small groups because even when dividing unique attributes, it is still inevitable that these small groups are not treated fairly by the model [20, 21].
Individual Fairness. Individual fairness notes that individuals must be treated consistently by the model [22, 23].
Comparison between Group & Individual Fairness. Group equity is more complex than individual equity because within groups there are different divisions and the division of groups can be flexible, that is, an individual can belong to different groups depending on the situation. different times [19]. In addition, group fairness does not consider the value of each individual and can lead to the selection of less qualified group members, whereas in theory individual fairness can be seen as a special case of group fairness, in which each individual belongs to a unique group.


2.2 Re-ranking Methods

 

Fig. 4. Illustrations for different re-ranking types

To encourage fairness, modify the models' main reranking technique. One of the best ways to improve the fairness of the results is to use reranking methods, since their outcomes are almost exactly the same as the final ones. Furthermore, this method has a minimal coupling to the model which means we will not need to influence the original model directly but only use the output of that model to re-rank it. This will help us avoid having to modify or improve the recommender model architecture. However, the effectiveness of the reordering method can be compromised because the number of base model outputs fed into the reordering stage is often very small., so the effectiveness of the reordering method may be hindered. Re-ranking methods are divided into three types: slot-wise, user-wise, and global-wise [24]. Figure 1 depicts the differences between the three types. But we will only cover user-wise and global-wise in this article.
2.3.1 User-wise. This method tries to directly find the best recommendation list for the user based on the optimization goal for the entire list. The re-ranking method is used for one recommendation list at a time.
2.3.2 Global-wise. In contrast to the above method, this method will re-rank multiple recommendation lists for multiple users at the same time.





2.3 Base Model

Cold-start Recommendation Models.  There are many cold start models but we cannot test them all. In general, algorithms can be classified into joint-training, separate-training, combined, contrastive learning, and heuristic non-parametric methods. Our work selects algorithms that have good performance and are easy to implement. The CCFCRec method is a Contrast Collaborative Filtering for Cold-Start item Recommendation which capitalizes on the co-occurrence collaborative signals in warm training data to alleviate the issue of blurry collaborative embeddings for cold-start item recommendation [18].  In addition, we also use another CLCRec method is a Contrast Learning-based method consisting of three components: contrastive pair organization, contrastive embedding, and contrastive optimization modules [19].


2.3.1 CLCRec


 

Fig. 5. Illustrations architecture of base model CLCRec

Contrastive Learning-based Cold-start Recommendation (CLCRec) consists of three main components. The first is contrastive pair organization. For U-I loss, Unobserved interactions are represented as negative user-item pairs, whereas past interactions are represented as positive user-item pairs. With 
R-E loss, One item is paired with itself, other items represent the positive and negative item-item pairs and both are subject to the self discrimination task. After setting up the contrastive pairs U-I and R-E, they will be embedded into contrastive embedding networks (CEN). The U-I CEN will be responsible for creating collaborative embeds for pairs of users and items. The R-E CEN contains an encoder that can be trained to find ways to represent features based on their content.
CLCRec is a framework composed of three parts: contrastive pair organization, contrastive embedding network, and contrastive optimization.
Contrastive Pair Organization. identify positive pairs constructed by cases semantically with some negative pairs concatenated by different patterns. Therefore, it is important to organize users and items in contrasting pairs U-I and R-E.
U-I Contrastive Pair. We consider pairs of user items observed in historical interactions as positive, as (𝑢,𝑖) shown in Figure 2. Meanwhile, we randomly sample 𝐾 items (e.g., 〖(j〗_1,j_2,...  ,j_K))  , have not been acquired by 𝑢 and pair the user to establish negative pairs, as shown in Figure 1. Formally, positive and negative U-I pairs can be defined as:

{(u,i),(u,j_1 ),(u,j_2 ),...,(u,j_K )}

Compared with negative pairs, positive pairs contain similar cooperative signals. Such comparison therefore facilitates the detection of collaborative signals conveyed by interactions.
R-E Contrastive Pair. Different from U-I pairs, R-E pairs apply a self-discrimination task to maximize the mutual information of two different representations of items. To construct the pairs, taking 𝑖 in Figure 2 as an example, we set it as the anchor item and connect the anchor with itself as a positive pair, which shows the semantic similarity between the two representations of the same one item. In contrast, negative pairs organized by anchors with other items are semantically different. As shown in Figure 2, we concatenate the items together to obtain the R-E pair:

{(i,i),(i,j_1 ),(i,j_2 ),...,(i,j_K )}

Where (𝑖,𝑖) is the positive pair and the others are negative ones.
Contrastive Embedding Network. Based on the contrast pairs, we create U-I and R-E contrast embedding networks (CEN) to represent users and items, and calculate the correlation of each pair using the predefined density ratio functions.
U-I Contrastive Embedding Network. To model collaboration signals from user-item interactions, we first fetch their id embeddings (e.g., e𝑢 and e𝑖 ) from a lookup table defined by the parameter matrix:

E = [e_(i_1 ),...,e_(i_N )  ,e_(u_1 ),...,e_(u_M ) ].

Then, a shared CF encoder is used to learn collaborative embeddings for users and items. It can be implemented using various models, such as MF-based, neural network-based models, and graph neural network-based models.
R-E Contrastive Embedding Network. This network is used to evaluate the correlation between two views of the items - collaboration signals and content information. It can be considered as two parallel paths to model the item's feature representation and collaborative embedding, respectively. The appropriate way to embed collaboration is similar to the corresponding activities in the U-I network.
Contrastive Optimization. To maximize mutual information implement a contrastive training strategy to optimize the model parameters. Combine the defined density ratio functions.


L = λL_RE+(1-λ) L_UI+η|(|Θ|)|_2^2   
   	     = -λ■(E@i∈Ι) [ln  exp⁡((z_i^T f_j)/(|(|z_i |)|· |(|f_j |)| )  · 1/τ  )/(exp⁡((z_i^T f_j)/(|(|z_i |)|· |(|f_j |)| )  · 1/τ  )+ ∑_(k=1)^k▒exp⁡((z_i^T f_j)/(|(|z_i |)|· |(|f_(j_k ) |)| )  · 1/τ  ) )]
                         - (1- λ) ■(E@(u,i)∈O)[ln exp((z_i^T z_u)/τ)/(exp((z_i^T z_u)/τ)+∑_(k=1)^k▒exp((z_(j_k)^T z_u)/τ) )]+ η|(|Θ|)|_2^2

L_(RE )and L_(UI )are used to represent the contrast loss to maximize the mutual information between R-E and U-I. L_(UI )has the same goal of optimizing Personalized Ranking (BPR) loss [25], and optimizes the recommendation model in an end-to-end manner without any other loss function. Use hyper parameter λ to balance collaborative filtering and feature representation.


2.3.2 CCFCRec

We use a model called Contrastive Collaborative Filtering for Cold Start item Recommendation (CCFCRec). The main idea is to teach the CF module to remember the collaboration signals that appeared during the training phase and fix the blurred CBCEs of cold start item in accordance with the remembered co-occurrence collaborative signals.
The contrast CF framework, which consists of a content CF module and a co-occurrence CF module, is the specific foundation upon which this approach operates. As a result, for a matching training item, CFCRec is able to produce a CBCE and a Co-Occurrence Collaborative Embedding (COCE). The problem occurs when co-occurrence collaborative signals are not active during the cold start process, it is replaced by including the co-occurrence collaborative signals into the content CF module during the training process where the co-occurrence collaborative signals are available for training items, instead of directly encoding them in CBCEs. CFCCRec uses complex contrastive learning to implement co-occurrence collaborative signals that are captured by COCE, remembered by the content CF module during the training phase, and made available during the application phase. This maximizes the information between the CBCE and COCE of an item. Within a multi-task learning framework, the two CF modules are jointly trained in tandem. Multi-task optimization ensures consistency in accurately predicting engagement probability performed by the content CF module and the co-occurrence CF module based on an item's CBCE and COCE, giving an advantage to the active transfer of co-occurring collaboration signals to the content CF module.


2.3.2.1 Problem Formulation

Let U and V is a set of users and set of items.
Let O={O_(u,v)} where O_(u,v) is the interaction between a user u ∈ U and an item v ∈ V.
Let V_u⊆ V  be the set of items that user u ∈ U interacted with and U_u⊆ U  be the set of users who interacted with items v ∈ V. For each item v iss associated with a attribute set X_v consiting of m attributes 〖{x〗_1^((v)),⋯ ,x_m^((v) )} , where an attribute is represented as one-hot vector, e.g., movie director, a multi-hot vector, e.g., movie genre, or a real valued vector, e.g., item image. 
Let x_i^((v) )  ∈ R^(d×1  )be the embedding of the ith attribute x_i^((v) ), where d is the dimensionality of embedding and i ≤i ≤m.
Given a warm training dataset D consisting of {U,V,O}, a cold-start item recommendation model to estimate the probability y ̂_(u,v)  that a user u will interact with an item v: y ̂_(u,v)=R(u,v,X_v), such that for any pair of u^+∈ U_v,u^-∉ U_v  in the training dataset, y ̂_(u^+,v) > y ̂_(u^-,v) .















2.3.2.2 CCFCRec Architecture

 

Fig. 6. Illustrations architecture of base model CCFCRec

In Figure 6, the content CF module includes the CBCE encoder g_c and the CBCE-based predictor f_q, the co-occurrence CF module includes the COCE Encode g_v and the COCE-based predictor f_z, and the UCE Encoder g_u  is shared between two CF modules.

Collaborative Embedding 
CBCE. Depending on how the attributes are encoded, first create the attribute embeddings 〖{x〗_i^((v) )} for a training item v, where i ≤i ≤m. Given that x_i^((v) ) is might be either a one-hot vector or multi-hot vector, then a lookup over a learnable embedding matrix W_i  ∈R^(d×|x_i^((v) ) |   )   can yield its attribute embedding, i.e., x_i^((v) )=W_i x_i^((v) ). If x_i^((v) ) is an image, the x_i^((v) ) is obtained using a convolutional network that has been trained beforehand, such as VGG []. When the feature embeddings 〖{x〗_i^((v) )} are ready, the content embedding
c_(v )∈R^(md×1  )be generated by a concatenation of 〖{x〗_i^((v) )}. At last, the CVCE q_v is produced via g_c with c_v as input:
q_v=g_c (c_v ), 	(1)

g_c build as a two-layer MLP with activation function LeakyReLU in order to capture the nonlinear interactions between attributes.

COCE and UCE. The COCE z_c and UCE s_u encode the preference of item v received from users and the preference of user u offered to items, by hidden co-occurrence collaborative signals in the observed interactions between users and items. As a result, the item v is represented by multi-hot vector
v ∈ 〖{0,1}〗^(|U|×1), and the u-th component v(u)=1 if u ∈ U_v, or else v(u)=0. In the same way, a user u is represented by a multi-hot vector u ∈ 〖{0,1}〗^(|V|×1), and the v-th component u(v)=1 if 
v ∈ V_u, or else u(v)=0. For the sake of clarity, the COCE endcode g_v and the UCE encode g_u are put into action as linear combination across embedding matrix columns, i.e.,

z_v=g_v (v)=W_v u, 	


s_u=g_u (u)=W_u u,  

Where W_v  ∈R^(d×|U|   )and W_u  ∈R^(d×|V|   ) are matrices can be learnable.

CBCE captures user preferences for item attributes, while COCE captures co-occurring collaboration signals from interactions. However, CBCE cannot be directly encoded because it only contains items from the training phase. So the content CF module will remember the collaboration signals that appear simultaneously in its parameters during the training phase, so that the content CF module can overcome the fuzzy CBCEs of the initial entries. Cold start involves memory during the application phase. The model built for the training item v, N_v^+={v^+:U_v∩U_(v^+ )≠∅} will be built as a positive sample set, meaning items that some users have interacted with v, and conversely it will be a negative sample set 〖N_v^-=V∖N〗_v^+. To maximize the mutual information between q_v  and z_(v^+ ) and minimize the mutual information between q_v  and z_(v^- ). The contrast loss function will be of the form:

L_c=-E_(v∈D,v^+∈ N_v^+ ) [ln exp(〈q_v,z_(v^+ ) 〉/τ)/(exp(〈q_v,z_(v^+ ) 〉/τ)+∑_(z_(v^- )∈〖 N〗_v^-)▒exp(〈q_v,z_(v^- ) 〉/τ) )],  

Where 〈∙,∙〉 represents inner product.

Interaction Prediction
During the training phase, CFCCRec will make two predictions about the probability of interaction between user u and an item v utilizing, respectively, the COCE-based predictor f_z  and the CBCE-based predictor f_q. Because of its simplicity, it will be implemented as a inner product prediction to rank the similarity of items and users.

y ̂_(u,v)^q=g_q (q_v,s_u )=〈q_v,s_u 〉,  

y ̂_(u,v)^z=g_q (z_v,s_u )=〈z_v,s_u 〉. 

For a training item v, each positive user u ∈ V_u shall be matched with a negative user u^-  from sample V∖V_u. Then, by applying the popular pairwise ranking loss BPR [25], the loss functions for the joint training of the two predictors will be of the form:

L_q=-∑_((v,u^+,u^-)∈D)▒lnσ(y ̂_(u^+,v)^q-y ̂_(u^-,v)^q ) ,  

L_z=-∑_((v,u^+,u^-)∈D)▒lnσ(y ̂_(u^+,v)^z-y ̂_(u^-,v)^z ) ,  

where σ is sigmoid function.
Notably, the two CF modules share the same UCE s_u and are joint trained with the same supervision. By offering a constant optimization objective, this kind of multi-task learning makes sure that co-occurrence collaboration signals are actively transferred to the content CF module.
Overall Loss Function
The overall loss function is defined as:

〖L=L〗_q+L_z+〖λL〗_c+‖Θ‖,  

Where λ is a component that regularizes the contrastive loss's contribution, and Θ represents the learnable parameters. Adam is choose for the optimizer.


2.4 Metrics

Now what do we use to evaluate the recommender system? Going through each question, we use four metrics to evaluate. We use Precision@K and Recall@K to evaluate the performance of recommender and ranking systems. Next use NDCG@K [26] to measure the quality of recommendation and information retrieval systems. Finally, to match our research goals, we use an additional metric called MDG [27].We will go through each metric below.


2.4.1 Precision@K

Precision@K measures how many items in a long-K list have the same ratio. Simply put, it shows us how many of the suggested or retrieved items are related to each other.
Formula of precision:

Precision@K=(Number of relevant item in K)/(Total number of item in K)

Where K is a rank that you can choose arbitrarily to limit your evaluation. Let's say we are going to show the top 10 recommendations on an e-commerce site, then the value will be Precision@10. Now we have a binary sticker called The Relevance, which represents the interaction between the user and the item more easily understood than when the user has clicked on the product or added it to the cart . Precision answers the question of how many items will fit the user? For example, out of 10 suggested items (interaction results), there are 3 items that are relevant to each other, then the value 
Precision@10 =  3/10  = 0.3.


2.4.2 Recall@K

Recall@K measures the ratio of relevant items identified in the top K recommendations to the total number of relevant items in the dataset. Simply put it allows us to find how many related items there are.
Formula of recall:

Recall@K=(Number of relevant item in K)/(Total number of relevant items)

Like Precision, K represents the cut-off point you consider for evaluation. Relevance is a binary label for situations like clicks, purchases, etc.


2.4.3 NDCG@K

NDCG@K stand for Normalized Discounted Cumulative Gain, it is a measure to evaluate the quality of recommendation and information retrieval systems. NDCG helps measure the ability to sort items based on relevance.
Formula of NDCG:

NDCG@K=(DCG@K)/(IDCG@K)

Where IDCG represent for a perfect ranking and DCG stand for Discounted Cumulative Gain. To calculate DCG we must identify related items that have less weight. This can usually be determined using a logarithmic penalty. The formula will take the form:

DCG@K=∑_(k=1)^K▒〖rel〗_i/log_2⁡〖(i+1)〗 

We can calculate it by divided each item’s gain with an increasing number as you proceed down the list, computed as an inverse logarithm of the position number. With 〖rel〗_i is the relevant score of item position i.

2.4.2 MDG

MDG is Mean Discounted Gain for an item i, it is a measure to calculate the true positve rate of an item.
Fomula of MDG:

〖MDG〗_i=1/|U_i^+ |  ∑_(u∈U_i^+)▒(δ(z ̂_(u,i)≤k))/(log⁡(1+z ̂_(u,i)))

Where U_i^+is a set of matched users for the new item i in the test set. z ̂_(u,i) is the ranking position of i for user u by a cold start recommendation. δ(x) return 1 if x is true, otherwise 0. Mean that we only consider the discounted gain 1/(log⁡(1+z ̂_(u,i))) for ranking position within the top-K recommendations. 〖MDG〗_i=0 denote the item i is never recommended. 〖MDG〗_i=1 denote the item i is ranked at the top position to match all user.

Rawlsian Max-Min fairness requires the model to maximize the minimum utility for the group so that no object is undeserved by the model. Unlike fairness concepts [28 - 35] these eliminate differences between groups but ignore disincentives for those who are better served. Max-min fairness does not require reducing the utility of the objects served but on the contrary it accepts inequity. So Max-min fairness is preferred in applications that do not need perfect equality, such as recommendation tasks, and it can also better preserve the overall model utility of our study. We are quite suitable for its application.

By apply Rawlsian Max-Min fairness to the MDG metric. We can calculate the average MDG of t% worst-off items, which are the t% item with lowest MDG during testing and higest MDG for best-served items. Our report denoted as MDG-min 10%, MDG-min 20% and MDG-max 10%.























Chapter 3

PROJECT MANAGEMENT PLAN



Project Timeline

Throughout the 15-week process we divided the work into three phases:
Preparation: We determine project goals, scope, resources, management methods and division of project tasks. We first determine what our research question is? What results do we want to achieve? Next we read research papers on the issues that we have oriented based on the research question. Once we identify those critical issues, we can easily learn and identify the relevant models and datasets that will be used throughout the project without deviating from our goals. This phase is important in setting the foundation for the entire project and ensuring that all team members are on the same page.
Development: We choose the proposed models based on the fact that they must be able to run the cold start problem with items based on the articles we have researched. Next focus on running those base models. In parallel with running those base models, we also research our new method with the input of the method being the output of the base model recommender. The purpose of those methods is to increase fairness for users. We will not mention it in this entry. Once satisfied with the model's performance, we deployed it to the web API we developed to share our work with the world and demonstrate its performance.
Wrapping up: We focus on completing all remaining documents, project timelines and deliverables. We also prepared a final presentation of our work, which showcased the achievements and values of the project.
Going deeper into our weekly project planning, important tasks and milestones have been broken down into smaller, more manageable chunks to ensure things get done consistently and smoothly. During the first week, we focused on defining the project's goals by formulating research questions, identifying relevant models and data sets, and conducting a review of the research literature. . We also develop a basic project plan, identify the management tools that will be used, and establish a timeline for the project. During the second week, we continued our literature review and began reading research papers in parallel with searching for data sets. This gave us a deeper understanding of the techniques used by people in their research papers which enabled us to inform our approach to the project. During the third week, we configured a suitable environment to train the model while continuing to explore the research on the technique used. This involves setting up the necessary hardware and software tools, as well as developing a plan for how to deploy and optimize the model. By the end of the third week, we had a solid foundation for the project, including a clear understanding of the goals, a clear plan, and the right environment to develop the model. From weeks 4 to 12, we enter a continuous training and improvement loop in which we continuously train our method on models and data sets and collect results output to improve our methods so that they are most effective. This process allows us to refine our method and ensure that it increases the effectiveness of the user recommendation process without any unfairness. During weeks 8 to 10, while the training round is still going on, we focus on learning about API deployment tools, which allow us to deploy our model as a web service and deploy it as an e-commerce platform. Finally, in weeks 10 to 12, we tested the model on the website we developed, using what we considered the best performing model to test the site. Is the website operating stably or not? This gives us the opportunity to see how well our method works in a real-world situation and identify any issues that require further improvement. At week 13, we finished coding and began preparing the final report. We reviewed the progress of the project, identified areas for improvement, and gathered all the necessary documents for the report. We also submitted all relevant resources after ensuring that our work was formatted correctly. In week 14, we practice our final report, practice our presentation, and make sure we can communicate our findings and results effectively. Finally, in week 15, we demonstrated our method via the website, discussed the results, and answered questions from the audience. A summary of the weekly plan can be seen in Table 3.1 and specific work of each member in Table 3.2.











         Table 3.1  Weekly Project Plan.
Week	Objectives
1	Determine goals by asking research questions, searching for related research on Risk-awareness and recommender systems. Develop basic project plans.
2	Read research papers in parallel with searching for relevant datasets.
3	Configure the environment suitable for model training while looking for more research on inference techniques.
4 - 12	Training and improvement loop in which we continuously train our method on models and data sets and collect results output to improve our methods so that they are most effective.
8 - 10	Learning about API deployment tools.
10 - 12	Tested the model on the website developed.
13	Finished coding and began preparing the final report.
14	Practice present for final report.
15	Present our work.






Table 3.2  Weekly Task Assignment.
Week	Nguyen Trong Quoc Dat	Nguyen Nhat Minh	Tran Le Anh Tuan
1	Determine the objectives, and find related research.	Determine the objectives, and find related research.	Determine the objectives, and find related research.
2	Read research papers.	Read research papers.	Find relevant datasets.
3	Research re ranking method. Find new method for reranking. Configure the environment suitable for model training. Prepare slide for review 1.	Research metric for fairness problem. Configure the environment suitable for model training. Prepare slide for review 1.
	Research what is cold start, warm start problem. Configure the environment suitable for model training. Prepare slide for review 1.
4	Run base model Heater.	
Run base model LightFM.
	Run base model GoRec.
5	Run method re-ranking on base model Heater.	Run method re-ranking on base model LightFM.	Run base model GoRec apply amazon datasets
6	Suggest idea for Inverse Propensity Weight method	Run base model lighFM with method Inverse propensity weight	Write Acknowledgements
7	Relax Linear Program with Python-MIP for optimization	Learn and run first step of front-end	Learn and run first step of back-end
8	Run Amazon datasets for base model, and create new method for re ranking.	Build interface for demo, and help Dat run datasets amazon.	Build SQL database for demo.
9	Experiment with contrastive learning. Prepare slide for review 2.	Write Introduction, Related work, Project management plan in report. Prepare slide for review 2.	Combine front-end with back-end. Prepare slide for review 2.
10	Run base model CLCRec. Format data	Write Materials and Methods.	Create function front-end: add, delete item, rating item.
11	Tesing new method, metric. Prepare slide for review 3.	Run base model Vae CF. Prepare slide for review 3.	Write Deployment: Interface, database, API. Prepare slide for review 3.
12	Run base model CCFCRec. Write Result, Appendix.	Run Heater model after format tensorflow 2. Write Discussion, Reference.	Run web demo. Write Conclusion.
13	Finish project, prepare slide for final report.	Finish project, prepare slide for final report.	Finish project, prepare slide for final report.
14	Practice present for final report.	Practice present for final report.	Practice present for final report.
15	Present our work.	Present our work.	Present our work.





















Chapter 4

MATERIAL 
AND METHODS



4.1 Materials

4.1.1 Hardware

Google Colaboratory
Google Colaboratory, is a free, cloud-based platform provided by Google that allows users to write and execute Python code collaboratively in a Jupyter Notebook environment. One  of the significant advantages of using Google Colab is that it provides free access to Graphics Processing Units (GPUs). This is particularly useful for machine learning tasks that involve heavy computational workloads, as these accelerators can significantly speed up the training of deep learning models. Also, Colab comes with several pre-installed libraries commonly used in data science and machine learning, such as TensorFlow, PyTorch, Keras, OpenCV, and more. This makes it convenient for us to start working on their projects without worrying about installing these libraries manually. However, we still face some inconvenience during the training process when using Colab. There is a limitation on GPUs and TPUs access for Colab’s users. For Colab's free plan, we can only have access to the Tesla T4 GPU, which still takes quite a long time for heavy computational workloads. Also, the provided VRAM for the Tesla T4 GPU is only 15GB, which causes us many inconveniences during the training process as for some models, they require more VRAM to train. Therefore, we have to reduce the batch size which will make the training process finish longer than we expected. Moreover, Colab for free-plan users only provides us with 6 hours of continuous usage which makes us have to  come up with a solution to save our model’s checkpoint so that we can continue the training  process the next day (or with a different account). Despite those drawbacks we have mentioned, Google Colab is still a great, powerful and useful platform for our model training process.


4.1.2 Data Management

Google Drive
Google Drive is a cloud-based file storage and synchronization service developed by Google. Google Drive provides users with free cloud storage space to store files such as documents, images, videos, and more. The free storage limit is typically generous, and additional storage can be purchased if needed. We use Google Drive as a platform for storing our management plan, our documents, slides for reviewing,v.v.


4.1.3 Libraries And Frameworks

PyTorch
PyTorch is an open-source machine learning library developed by Facebook’s AI Research lab (FAIR). It is widely used for deep learning and artificial intelligence applications. PyTorch is known for its dynamic computational graph, which makes it particularly well-suited for research and experimentation. PyTorch offers various libraries and tools to support different aspects of machine learning and deep learning. We used some functions of Pytorch to perform many parts in both our training phase and deployment phase.

TensorFlow
TensorFlow is an end-to-end platform for machine learning. The ecosystem is built on the Core framework that streamlines model building, training, and export. TensorFlow supports distributed training, immediate model iteration, and easy debugging with Keras, etc.

FastAPI
FastAPI is a modern, fast (as the name implies), web framework for building APIs. FastAPI automatically generates interactive API documentation (Open API) based on the Python type hints used in the code. This helps developers understand the API’s structure and use it effectively. Also, FastAPI is designed for performance and utilizes asynchronous programming to handle multiple requests efficiently. It is one of the fastest Python web frameworks, making it ideal for building high-traffic APIs. We used FastAPI to build some APIs for our deployment process.


4.4 Methods


4.2.1 Datasets

Amazon datasets. Amazon Review is a dataset to tackle the task of identifying whether the sentiment of a product review is positive or negative. This dataset includes reviews from four different merchandise categories: Books (B) (2834 samples), DVDs (D) (1199 samples), Electronics (E) (1883 samples), and Kitchen and housewares (K) (1755 samples).
MovieLens 1M. MovieLens 1M movie ratings. Stable benchmark dataset. 1 million ratings from 6000 users on 4000 movies.


4.2.2 Algorithm

The goal for addressing equity would be the ideal distribution of exposure or relatedness across groups. Here we will divide it into two groups: producer and customer.

Fairness constraint on producers side. According to CFair's authors[36]. Fairness is expressed through two functions: exposure and relevance, which both can be binary or graded [37]. The main goal of this is to provide product visibility so will only focus on the binary aspect. To mesure it, they divide items into two types: short-head  I_1 and long-tail  I_2, defined based on popularity score where I_1∩ I_2=∅. They defined as MP the symbol to measure the visibility of groups of items in the recommendation list decision, and A as the number of times the groups of items were shown. Deviation from Producer Fairness (DPF):

DPF(A,I_1,I_2 )=E[MP(i,A)|i∈I_1 ]-E[MP(i,A)|i∈I_2 ]

Fairness constraint on customer side. Divided into two user groups with  U_1 being the frequent user group and U_2 the less frequent user group and we define U_1 and U_2 based on their activity level. MC is a metric that can evaluate the relevance of recommendations in each group based on the recommendation list matrix, A, such as NDCG, Recall, or F1 groups. Ideally fair recommendations recommend inks based on the known preferences of frequent and less frequent users that will not be exaggerated by the recommendation system's algorithm. We will define the deviation from user fairness as:

DCF(A,U_1,U_2 )=E[MC(u,A)|u∈U_1 ]-E[MC(u,A)|i∈U_2 ]

Note that when the values 𝐷𝑃𝐹 → 0 or 𝐷C𝐹 → 0, it represents equality between advantaged and disadvantaged user groups and item groups. However, in our method we will only use DPF, so we will focus on the problem 𝐷𝑃𝐹 → 0. When the value is greater than 0 this indicates differential reduction or unfair treatment between Different groups of providers in the referral system. A lower DPF value indicates that recommendations are being distributed more equitably among different groups of providers, leading to a fairer representation of items from different sources. This DPF reduction is intended to provide a more balanced and unbiased allocation of access to providers, promoting fairness in the proposal process.
We use the top-N recommendation and relevance scores by traditional unfair recommeder system. We use re ranking posts to maximize relevance scores while minimizing bias due to fairness based on the DPF manufacturer's perspective. We will construct the fairness-aware optimization problem for the binary matrix, A, as follows:

(max)┬(A_ui ) ∑_(u∈U)▒∑_(i=1)^N▒〖S_ui∙A_ui-λ∙DPF(A,I_1,I_2 ) 〗
s.t.∑_(i=1)^N▒〖A_ui=K,〗  A_ui∈{0,1}

The solution above will recommend exactly K items to each user while maximizing the total preference score and penalizing deviations from fairness. The hyperparameter λ ≤ 1 will be chosen based on the application and will assign weight to the user based on their interests. 





Chapter 5

RESULT




Table 5. Comparation
Base Model	Method	Recall	Precision	NDCG@K	Fairness:MDG
CCFCRec					
CLCRec					
					



































Chapter 6

DISCUSSION



 





Chapter 7

DEPLOYMENT



7.1 Server

For the demo deployment, we use Django, a Python web framework, to showcase our application on a local server. This allows us to easily demonstrate and test the functionality of the systems. 


7.2 Database

In our Django e-commerce website, we use SQLite as our database management system. SQLite stores data in a structured format, organized into tables, rows, and columns. Each table represents a specific entity in our website, such as products, interactions, and users. We establish relationships between entities using foreign key constraints.

The database stores essential information about products, users, and interactions. For example, the Products table contains details such as product name, category, price, description, and image path. The Interactions panel links users to the products they interacted with along with timestamps.
 
SQLite's convenience makes it portable and easy to manage, while Django's ORM simplifies database interactions by abstracting away the underlying operations. Overall, our database supports efficient data storage, retrieval and manipulation, ensuring the smooth operation of our e-commerce platform.
7.3 Platform Flowchart 

In the workflow of our e-commerce website, there is a continuous process from the initial user interaction until they receive the final result. Users start by logging in to the website, browsing products, or taking actions like adding items to the cart or placing an order. The front-end server handles these requests by providing corresponding HTML templates. Upon receiving a request, the backend server interacts with the database to retrieve product information or update the user's shopping cart. The backend server then executes business logic, such as pricing, inventory management, and user authentication. The response from the backend server contains data that is returned to the frontend server, where the data is rendered and displayed on the user's browser. This process continues as the user continues to interact with the website, creating a continuous and repetitive workflow.


7.4 UI

7.4.1 Homepage

Our home page is shown in Figure 7. In this page, we will introduce about products and the details for each of them. User can click on “View” of each products to see more.


 


Fig. 7. Homepage of our E-commerce website


7.4.2 Recommendation page

In this page, user can adjust the number of suggested products and the minimum interaction required for each of them. When user clicks on “Recommend” button, our model will generate on the back-end then output the results. Besides, our system will also provide a comparison between Recommendation with and without fairness. The Recommendation page will be shown in Figure 8.



 


Fig. 8. Recommendation page













7.4.3 Interaction history page

This page will display a history of products the user has interacted with. This page will be displayed in Figure 9.


 


Fig. 9. Interaction history page














Chapter 8

CONCLUSION


After what we researched and tested, we have proposed a new solution to the task of solving the fairness item problem for the recommender system.

8.1 

 
 




Appendix A


Failed Experiments
We tried a few other approaches in addition to the primary one that was previously suggested, but they did not work for various reasons, such as not enough memory or worse outcomes. The first method yields a worse outcome by using the DPF metric rather than the additional limitation. Secondly, we employ the direct metric MDG constraint; however, its implementation is rather intricate, and our system lacks the memory to employ that technique.
 




Appendix B


Source Code And Datasets
Table B.1 Source
CLCRec base model	https://github.com/datn2107/CLCRec
CCFCRec base model 	https://github.com/datn2107/CCFCRec
Process datasets and method	https://drive.google.com/drive/folders/1MumAOuO6em8QS4aWj_N9ZsDmJXvm7C5u?usp=drive_link









Appendix C


Import Base Model

In the process of searching for base models of the recommendation system, we acknowledged that using 5 base models, however, most of these models have trouble with pre-processing issues. We will show it in table C.1. With “-“ is don’t have, “√“ is have. From best of our knowledge, only CLCRec and CCFCRec suitable for our project. 




























REFERENCES

	Loren Terveen and Will Hill. Beyond Recommender Systems: Helping People Help Each Other. In HCI In The New Millennium, Jack Carroll, ed., Addision-Wesley, 2011.
	Badrul Sarwar, George Karypis, Joseph Konstan, John Riedl. Item-based collaborative filtering recommendation algorithms. WWW '01: Proceedings of the 10th international conference on World Wide Web. 2001. Pages 285-295.
	G. Linden, B. Smith, J. York. Amazon.com recommendations: item-to-item collaborative filtering. In IEEE Internet Computing. Jan-Feb. 2003 Pages 76-80.
	Djallel Bouneffouf. DRARS, A Dynamic Risk-Aware Recommender System. Computation and Language [cs.CL]. Institut National des Télécommunications, 2013. English. NNT: . tel-01026136.
	Alex Beutel, Jilin Chen, Tulsee Doshi, Hai Qian, Li Wei, Yi Wu, Lukasz Heldt, Zhe Zhao, Lichan Hong, Ed H Chi, et al. 2019. Fairness in recommendation ranking through pairwise comparisons. In Proceedings of the 25th ACM SIGKDD International Conference on Knowledge Discovery & Data Mining. 2212–2220.
	Robin Burke. 2017. Multi Sided fairness for recommendation. arXiv preprint arXiv:1707.00093 (2017).
	Sahin Cem Geyik, Stuart Ambler, and Krishnaram Kenthapadi. 2019. Fairnessaware ranking in search & recommendation systems with application to linkedin talent search. In Proceedings of the 25th ACM SIGKDD International Conference on Knowledge Discovery & Data Mining. 2221–2231.
	Ziwei Zhu, Xia Hu, and James Caverlee. 2018. Fairness-aware tensor-based recommendation. In Proceedings of the 27th ACM International Conference on Information and Knowledge Management. 1153–1162.
	Ziwei Zhu, Jianling Wang, and James Caverlee. 2020. Measuring and Mitigating Item Under-Recommendation Bias in Personalized Ranking Systems. In Proceedings of the 43rd International ACM SIGIR Conference on Research and Development in Information Retrieval. 449–458.
	Iman Barjasteh, Rana Forsati, Farzan Masrour, Abdol-Hossein Esfahanian, and Hayder Radha. 2015. Cold-start item and user recommendation with decoupled completion and transduction. In Proceedings of the 9th ACM Conference on Recommender Systems. ACM, 91–98.
	Zeno Gantner, Lucas Drumond, Christoph Freudenthaler, Steffen Rendle, and Lars Schmidt-Thieme. 2010. Learning Attribute-to-Feature Mappings for Cold-Start Recommendations.. In ICDM, Vol. 10. Citeseer, 176–185.
	Martin Saveski and Amin Mantrach. 2014. Item cold-start recommendations: learning local collective embeddings. In Proceedings of the 8th ACM Conference on Recommender systems. ACM, 89–96.
	Ajit P Singh and Geoffrey J Gordon. 2008. Relational learning via collective matrix factorization. Proceedings of the 14th ACM SIGKDD international conference on Knowledge discovery and data mining. ACM, 650–658.
	Aaron Van den Oord, Sander Dieleman, and Benjamin Schrauwen. 2013. Deep content-based music recommendation. In Advances in Neural Information Processing Systems. 2643–2651.
	Jingjing Li, Mengmeng Jing, Ke Lu, Lei Zhu, Yang Yang, and Zi Huang. 2019. From Zero-Shot Learning to Cold-Start Recommendation. In Proceedings of the AAAI Conference on Artificial Intelligence.
	Suvash Sedhain, Aditya Krishna Menon, Scott Sanner, Lexing Xie, and Darius Braziunas. 2017. Low-rank linear cold-start recommendation from social data. In Thirty-First AAAI Conference on Artificial Intelligence.
	Maksims Volkovs, Guangwei Yu, and Tomi Poutanen. 2017. Dropoutnet: Addressing cold start in recommender systems. In Advances in Neural Information Processing Systems. 4957–4966.
	Zhihui Zhou, Lilin Zhang, and Ning Yang. 2023. Contrastive Collaborative Filtering for Cold Start  item Recommendation. DOI: https://doi.org/10.1145/3543507.3583286.
	Yinwei Wei, Xiang Wang, Qi Li, Liqiang Nie, Yan Li, Xuanping Li, and TatSeng Chua. 2018. Contrastive Learning for Cold-Start Recommendation. In Woodstock ’18: ACM Symposium on Neural Gaze Detection, June 03–05, 2018, Woodstock, NY . ACM, New York, NY, USA, 10 pages. https://doi.org/10.1145/ 1122445.1122456.
	Michael Kearns, Seth Neel, Aaron Roth, and Zhiwei Steven Wu. 2018. Preventing fairness gerrymandering: Auditing and learning for subgroup fairness. In Proceedings of the International Conference on Machine Learning. PMLR, 2564–2572.
	Michael Kearns, Seth Neel, Aaron Roth, and Zhiwei Steven Wu. 2019. An empirical study of rich subgroup fairness for machine learning. In Proceedings of the Conference on Fairness, Accountability, and Transparency. 100–109.
	Asia J. Biega, Krishna P. Gummadi, and Gerhard Weikum. 2018. Equity of attention: Amortizing individual fairness in rankings. Proceedings of the 41st International ACM SIGIR Conference on Research & Development in Information Retrieval (SIGIR’18). Association for Computing Machinery, New York, NY, 405–414. DOI:https://doi.org/10.1145/ 3209978.3210063
	Cynthia Dwork, Moritz Hardt, Toniann Pitassi, Omer Reingold, and Richard Zemel. 2012. Fairness through awareness. In Proceedings of the 3rd Innovations in Theoretical Computer Science Conference (ITCS’12). Association for Computing Machinery, New York, NY, 214–226. DOI:https://doi.org/10.1145/2090236.2090255
	Yifan Wang, Weizhi Ma, Min Zhang, Yiqun Liu, and Shaoping Ma. 2023. A Survey on the Fairness of Recommender Systems. ACM Trans. Inf. Syst. 41, 3, Article 52 (February 2023), 43 pages. https://doi.org/10.1145/3547333. 
	Steffen Rendle, Christoph Freudenthaler, Zeno Gantner, and Lars Schmidt-Thieme. 2009. BPR: Bayesian personalized ranking from implicit feedback. Proceedings of Conference on Uncertainty in Artificial Intelligence, 452–461.
	Yining Wang, Liwei Wang, Yuanzhi Li, Di He, Tie-Yan Liu, Wei Chen. A Theoretical Analysis of NDCG Type Ranking Measures. DOI: https://doi.org/10.48550/arXiv.1304.6480.
	Ziwei Zhu, Jingu Kim, Trung Nguyen, Aish Fenton, and James Caverlee.  2021. Fairness among New Items in Cold Start Recommender Systems. In  Proceedings of the 44th International ACM SIGIR Conference on Research and  Development in Information Retrieval (SIGIR ’21), July 11–15, 2021, Virtual  Event, Canada. ACM, New York, NY, USA, 10 pages.  https://doi.org/10.1145/ 3404835.3462948.
	Alex Beutel, Jilin Chen, Tulsee Doshi, Hai Qian, Li Wei, Yi Wu, Lukasz Heldt, Zhe Zhao, Lichan Hong, Ed H Chi, et al. 2019. Fairness in recommendation ranking through pairwise comparisons. In Proceedings of the 25th ACM SIGKDD International Conference on Knowledge Discovery & Data Mining. 2212–2220.
	Sahin Cem Geyik, Stuart Ambler, and Krishnaram Kenthapadi. 2019. Fairnessaware ranking in search & recommendation systems with application to linkedin talent search. In Proceedings of the 25th ACM SIGKDD International Conference on Knowledge Discovery & Data Mining. 2221–2231.
	Toshihiro Kamishima and Shotaro Akaho. 2017. Considerations on Recommendation Independence for a Find-Good-Items Task. (2017).
	T Kamishima, S Akaho, H Asoh, and J Sakuma. 2013. Efficiency Improvement of Neutrality-Enhanced Recommendation.. In Decisions@RecSys.
	Toshihiro Kamishima, S Akaho, H Asoh, and J Sakuma. 2018. Recommendation Independence. In Conference on Fairness, Accountability and Transparency.
	T Kamishima, S Akaho, H Asoh, and I Sato. [n.d.]. Model-based approaches for independence-enhanced recommendation. In 2016 IEEE 16th International Conference on Data Mining Workshops (ICDMW).
	Flavien Prost, Hai Qian, Qiuwen Chen, Ed H Chi, Jilin Chen, and Alex Beutel. 2019. Toward a better trade-off between performance and fairness with kernel-based distribution matching. arXiv preprint arXiv:1910.11779 (2019).
	Andriy Mnih and Russ R Salakhutdinov. 2008. Probabilistic matrix factorization. In Advances in neural information processing systems. 1257–1264.
	Mohammadmehdi Naghiaei, Hossein A. Rahmani, and Yashar Deldjoo. 2022.  CPFair: Personalized Consumer and Producer Fairness Re-ranking for Recommender Systems. In Proceedings of the 45th International ACM SIGIR  Conference on Research and Development in Information Retrieval (SIGIR  ’22), July 11–15, 2022, Madrid, Spain. ACM, New York, NY, USA, 10 pages. https://doi.org/10.1145/3477495.3531959.




