# Condor

[![arXiv](https://img.shields.io/badge/arXiv-2501.12273-b31b1b.svg)](https://arxiv.org/abs/2501.12273)
[![license](https://img.shields.io/github/license/InternLM/opencompass.svg)](./LICENSE)

## ✨ Introduction  

[[🤗 HuggingFace Models](https://huggingface.co/internlm/)]
[[🤗 HuggingFace Datasets](https://hf.co/datasets/internlm/Condor-SFT-20K)]
[[📃 Paper](./assets/CondorPaper.pdf)]
<!-- [[📃 Paper](https://arxiv.org/abs/)] -->
<!-- [[🧰 OpenXLab](https://openxlab.org.cn/models/detail/OpenLMLab/)] -->
<!-- [[🌐 Project Page](https://internlm.github.io/)] -->

> The quality of Supervised Fine-Tuning (SFT) data plays a critical role in enhancing the conversational capabilities of Large Language Models (LLMs).
> However, as LLMs become more advanced, 
> the availability of high-quality human-annotated SFT data has become a significant bottleneck, 
> necessitating a greater reliance on synthetic training data. 
> In this work, we introduce \textbf{Condor}, 
> a novel two-stage synthetic data generation framework that incorporates  \textbf{World Knowledge Tree} and \textbf{Self-Reflection Refinement} to produce high-quality SFT data at scale. 
> Our experimental results demonstrate that a base model fine-tuned on only 20K Condor-generated samples achieves superior performance compared to % RLHF-trained 
> counterparts. 
> The additional refinement stage in Condor further enables iterative self-improvement for LLMs at various scales (up to 72B), 
> validating the effectiveness of our approach. 
> Furthermore, our investigation into the scaling for synthetic data in post-training reveals substantial unexplored potential for performance improvements, 
> opening promising avenues for future research.

## 🦅 Condor

Condor is a two-stage data synthesis engine adopted in InternLM3, designed to generate high-quality data for supervised fine-tuning of large language models (LLMs). The human-preference performance of the model improves significantly when fine-tuned with Condor, without affecting the model's knowledge capacity. The Condor pipeline is divided into two stages: data synthesis and data refinement. 

- **Condor Void (Data Synthesis):**

  During the data synthesis stage, Condor introduces the \textbf{World Knowledge Tree}, which serves as a foundation of tags for data generation. Next, we apply task and difficulty expansion to enhance the diversity and complexity of questions under each tag, leading to the creation of the initial synthetic QA dataset.

- **Condor Refine (Data Refinement):**

  In the data refinement stage, Condor employs a \textbf{Self-Reflection Refinement} strategy, allowing the model to iteratively optimize the responses by generating new critiques and obtain the final refined dataset.

## 🌟 Tag for Data Generation

<details><summary>click to expand</summary>
  
```json{
        "Marriage and Relationships": {
            "Dating and Friendship": ["Dating Platforms", "Dating Tips", "Dating Events"],
            "Marriage Management": ["Marital Relationships", "Marriage Law", "Marriage Counseling"],
            "Wedding Planning": ["Wedding Planning", "Wedding Photography", "Wedding Venues"],
            "Relationship Psychology": ["Relationship Psychology", "Communication Skills in Relationships", "Relationship Maintenance"],
            "Emotional Counseling": ["Solving Emotional Issues", "Emotional Repair", "Emotional Growth"],
            "Pre-Marriage Education": ["Pre-Marriage Preparation", "Pre-Marriage Psychology", "Pre-Marriage Legal Knowledge"]
        },
        "Entertainment Gossip": {
            "Celebrity News": ["Celebrity News", "Celebrity Interviews", "Celebrity Charity Events"],
            "Variety Shows": ["Show Recommendations", "Behind the Scenes", "Show Interaction"],
            "Film and TV Reviews": ["Movie Reviews", "TV Series Reviews", "Critics’ Opinions"],
            "Entertainment News": ["Latest Entertainment News", "Entertainment Events", "Exclusive Interviews"],
            "Fan Culture": ["Fan Activities", "Fan Support", "Fan Interactions"],
            "Gossip": ["Celebrity Gossip", "Entertainment Industry Secrets", "Gossip Chasing"]
        },
        "Artificial Intelligence": {
            "Machine Learning": ["Algorithm Principles", "Application Cases", "Learning Resources"],
            "Deep Learning": ["Neural Networks", "Deep Learning Frameworks", "Deep Learning Applications"],
            "Natural Language Processing": ["Language Models", "Text Analysis", "Dialogue Systems"],
            "Computer Vision": ["Image Recognition", "Video Processing", "Vision Algorithms"],
            "Intelligent Robotics": ["Robotics Technology", "Service Robots", "Industrial Robots"],
            "Autonomous Driving": ["Autonomous Driving Technology", "Autonomous Driving Regulations", "Autonomous Driving Testing"]
        },
        "Healthcare": {
            "Disease Prevention and Treatment": ["Common Diseases", "Preventive Measures", "Disease Treatment"],
            "Health and Wellness": ["Dietary Wellness", "Exercise Wellness", "Traditional Chinese Medicine Wellness"],
            "Psychological Counseling": ["Mental Health Issues", "Psychological Therapy", "Psychological Adjustment"],
            "Medical Technology": ["Medical Equipment", "Medical Technology", "Medical Innovation"],
            "Health Insurance": ["Types of Insurance", "Insurance Choices", "Insurance Claims"],
            "Fitness": ["Fitness Methods", "Fitness Equipment", "Fitness Diet"]
        },
        "Pets": {
            "Pet Care": ["Daily Pet Care", "Pet Nutrition", "Pet Behavior"],
            "Pet Medical Care": ["Pet Diseases", "Pet First Aid", "Pet Hospitals"],
            "Pet Training": ["Basic Training", "Behavior Correction", "Training Techniques"],
            "Pet Supplies": ["Toys", "Food", "Care Products"],
            "Pet Adoption": ["Adoption Procedures", "Adoption Conditions", "Adoption Events"],
            "Pet Activities": ["Pet Competitions", "Pet Gatherings", "Pet Festivals"]
        },
        "Environment": {
            "Environmental Protection": ["Ecological Protection", "Pollution Control", "Environmental Monitoring"],
            "Sustainable Development": ["Green Energy", "Circular Economy", "Ecological Agriculture"],
            "Energy Conservation and Emission Reduction": ["Energy-Saving Technology", "Emission Reduction Policies", "Low-Carbon Life"],
            "Waste Sorting": ["Sorting Standards", "Sorting Methods", "Recycling"],
            "Environmental Policies": ["Policy Regulations", "Policy Interpretation", "Policy Impact"],
            "Green Living": ["Green Consumption", "Green Travel", "Green Buildings"]
        },
        "Technology": {
            "Internet": ["Network Technology", "Cybersecurity", "Online Services"],
            "5G Communication": ["5G Technology", "5G Applications", "5G Devices"],
            "Blockchain": ["Blockchain Principles", "Blockchain Applications", "Digital Currency"],
            "Artificial Intelligence": ["AI Technology", "AI Ethics", "AI Industry Applications"],
            "Aerospace": ["Aerospace Technology", "Aircraft", "Space Exploration"],
            "New Energy": ["Solar Energy", "Wind Energy", "New Energy Vehicles", "Energy Storage"]
        },
        "Education and Training": {
            "Preschool Education": ["Choosing Kindergartens", "Early Childhood Education", "Preschool Education Policies"],
            "K12 Education": ["Primary Education", "Secondary Education", "Family Education Guidance"],
            "Higher Education": ["University Major Selection", "Graduate Education", "Higher Education Policies"],
            "Vocational Training": ["Vocational Skills Training", "Professional Certifications", "Career Development Planning"],
            "Online Education": ["Online Course Recommendations", "Distance Education", "Online Learning Tips"],
            "Study Abroad and Immigration": ["Study Abroad Consultation", "Immigration Policies", "Overseas Living Guide"]
        },
        "Career Development": {
            "Career Planning": ["Career Positioning", "Career Development Paths", "Career Transition Guidance"],
            "Job Search Skills": ["Resume Writing", "Interview Skills", "Job Search Channels"],
            "Career Advancement": ["Promotion Strategies", "Workplace Performance", "Leadership Development"],
            "Interpersonal Relationships": ["Colleague Interaction", "Workplace Communication", "Workplace Etiquette"],
            "Entrepreneurship Guidance": ["Entrepreneurship Plans", "Entrepreneurship Resources", "Entrepreneurship Risk Management"],
            "Team Management": ["Team Building", "Team Collaboration", "Team Performance Management"]
        },
        "Finance and Investment": {
            "Stocks": ["Stock Market Analysis", "Stock Investment Strategies", "Stock Research"],
            "Funds": ["Fund Selection", "Systematic Investment Plans", "Fund Risk Management"],
            "Futures": ["Futures Market", "Futures Trading Skills", "Futures Risk Control"],
            "Foreign Exchange": ["Forex Trading", "Forex Market Analysis", "Forex Risk Management"],
            "Insurance": ["Insurance Product Selection", "Insurance Planning", "Insurance Claims"],
            "Financial Planning": ["Personal Finance", "Asset Allocation", "Retirement Planning"]
        },
        "Real Estate and Home Living": {
            "Real Estate Market": ["Market Trends", "Property Price Analysis", "Real Estate Policy Interpretation"],
            "Home Buying Guide": ["Home Selection Tips", "Home Buying Process", "Mortgage Application"],
            "Interior Design": ["Decorating Styles", "Decorating Materials", "Decorating Budget"],
            "Home Living": ["Home Arrangement", "Home Maintenance", "Smart Homes"],
            "Real Estate Policies": ["Policy Updates", "Policy Interpretation", "Policy Impact"],
            "Rental Market": ["Rental Process", "Rental Agreements", "Rental Tips"]
        },
        "Travel and Adventure": {
            "Domestic Travel": ["Destination Recommendations", "Domestic Travel Guides", "Travel Safety"],
            "International Travel": ["Visa Applications", "International Travel Guides", "Cultural Adaptation"],
            "Outdoor Adventures": ["Hiking", "Mountain Climbing", "Wilderness Survival Skills"],
            "Travel Guides": ["Travel Planning", "Travel Budget", "Travel Packing Lists"],
            "Travel Equipment": ["Backpack Selection", "Outdoor Gear", "Travel Essentials"],
            "Travel Photography": ["Photography Tips", "Travel Photography Works", "Photography Equipment Recommendations"]
        },
        "Food and Cooking": {
            "Food Recommendations": ["Local Delicacies", "Food Rankings", "Restaurant Recommendations"],
            "Cooking Skills": ["Basic Cooking", "Creative Cooking", "Cooking Tool Usage"],
            "Ingredient Selection": ["Ingredient Selection Tips", "Seasonal Ingredients", "Organic Ingredients"],
            "Food Culture": ["Food Culture", "Local Food Customs", "Dietary Health"],
            "Healthy Eating": ["Balanced Nutrition", "Healthy Recipes", "Dietary Wellness"],
            "Baking and Desserts": ["Dessert Making", "Baking Skills", "Dessert Ingredients"]
        },
        "Culture and Arts": {
            "Literature": ["Literary Works", "Literary Criticism", "Creative Writing Skills"],
            "Music": ["Music Styles", "Music Production", "Music Appreciation"],
            "Painting": ["Painting Techniques", "Painting Schools", "Painting Appreciation"],
            "Sculpture": ["Sculpture Art", "Sculpture Creation", "Sculpture Materials"],
            "Theater": ["Theater Performance", "Theater Creation", "Theater History"],
            "Film": ["Film Recommendations", "Film Reviews", "Film Production"]
        },
        "Sports and Fitness": {
            "Sports Events": ["Event Broadcasts", "Event Analysis", "Event History"],
            "Fitness Methods": ["Fitness Tutorials", "Fitness Plans", "Fitness Diet"],
            "Sports Equipment": ["Equipment Recommendations", "Equipment Usage", "Equipment Maintenance"],
            "Sports Celebrities": ["Celebrity Introductions", "Celebrity Interviews", "Celebrity Events"],
            "Sports Policies": ["Policy Interpretation", "Policy Impact", "Policy Updates"],
            "Sports Industry": ["Industry Trends", "Industry Investment", "Industry Cases"]
        },
        "Military and National Defense": {
            "Military News": ["News Reports", "News Analysis", "Military Updates"],
            "Defense Technology": ["Technology Advancements", "Technology Applications", "Innovative Technologies"],
            "Weapons and Equipment": ["Equipment Introduction", "Equipment Comparison", "Equipment Maintenance"],
            "Military History": ["Historical Events", "Historical Battles", "Historical Figures"],
            "Military Service System": ["Service Regulations", "Enlistment Process", "Veterans' Policies"],
            "National Security": ["Security Policies", "Security Education", "Security Awareness"]
        },
        "Social Welfare": {
            "Charity Donations": ["Donation Channels", "Donation Impact", "Donation Stories"],
            "Volunteer Services": ["Service Projects", "Service Training", "Volunteer Stories"],
            "Public Welfare Activities": ["Activity Organization", "Activity Participation", "Activity Impact"],
            "Public Welfare Organizations": ["Organization Introductions", "Organization Activities", "Organization Cooperation"],
            "Social Assistance": ["Assistance Targets", "Assistance Methods", "Assistance Policies"],
            "Spreading Love": ["Spreading Methods", "Spreading Activities", "Spreading Impact"]
        },
        "Automotive and Transportation": {
            "Automotive News": ["New Car Releases", "Car Reviews", "Automotive Trends"],
            "Driving Skills": ["Safe Driving", "Fuel-Efficient Driving", "Driver Training"],
            "Vehicle Maintenance": ["Routine Maintenance", "Fault Diagnosis", "Repair Services"],
            "Traffic Laws": ["Law Interpretation", "Safety Education", "Law Updates"],
            "New Energy Vehicles": ["Technical Features", "Market Dynamics", "Policy Support"],
            "Smart Transportation": ["Technology Applications", "Smart Systems", "Future Trends"]
        },
        "E-commerce": {
            "Online Shopping": ["Shopping Guides", "User Reviews", "Promotions"],
            "E-commerce Operations": ["Operations Management", "Market Analysis", "Customer Service"],
            "Cross-border E-commerce": ["International Logistics", "Tariff Policies", "Market Analysis"],
            "E-commerce Policies": ["Policy Interpretation", "Policy Impact", "Compliance Operations"],
            "E-commerce Marketing": ["Marketing Strategies", "Advertising Placement", "User Analysis"],
            "E-commerce Logistics": ["Logistics Delivery", "Inventory Management", "Logistics Technology"]
        },
        "Gaming and Animation": {
            "Online Games": ["Popular Games", "Game Reviews", "Gaming Communities"],
            "Single-player Games": ["Classic Games", "Game Guides", "Game Recommendations"],
            "Animation Works": ["Popular Anime", "Anime Characters", "Anime Production"],
            "Game Guides": ["Guide Sharing", "Skill Exchange", "Guide Videos"],
            "Animation Industry": ["Industry Trends", "Market Analysis", "Industry Policies"],
            "Game Merchandise": ["Merchandise Products", "Collecting Guides", "Merchandise Events"]
        },
        "Infant and Child Education": {
            "Early Education": ["Educational Philosophy", "Educational Methods", "Educational Toys"],
            "Maternal and Infant Care": ["Care Knowledge", "Care Skills", "Care Products"],
            "Child Psychology": ["Psychological Development", "Emotion Management", "Psychological Counseling"],
            "Parent-child Relationship": ["Parent-child Activities", "Parent-child Communication", "Parent-child Education"],
            "Baby Products": ["Product Selection", "Safety Standards", "Product Recommendations"],
            "Child Health": ["Healthy Growth", "Nutritional Diet", "Disease Prevention"]
        },
        "Senior Life": {
            "Elderly Care Policies": ["Policy Interpretation", "Policy Consultation", "Policy Implementation"],
            "Senior Health": ["Health Checkups", "Disease Prevention", "Healthy Eating"],
            "Senior Activities": ["Cultural Activities", "Sports Activities", "Social Activities"],
            "Senior Psychology": ["Psychological Adjustment", "Psychological Health", "Psychological Support"],
            "Elderly Care Institutions": ["Institution Selection", "Service Quality", "Institution Evaluation"],
            "Senior Products": ["Assistance Products", "Health Products", "Living Products"]
        },
        "Psychological Counseling": {
            "Mental Health": ["Mental Maintenance", "Mental Problem Prevention", "Mental Health Education"],
            "Psychological Disorders": ["Disorder Identification", "Disorder Treatment", "Disorder Management"],
            "Counseling Skills": ["Counseling Methods", "Communication Skills", "Case Studies"],
            "Psychological Tests": ["Test Types", "Test Applications", "Test Interpretation"],
            "Psychological Research": ["Research Trends", "Research Methods", "Research Results"],
            "Psychological Guidance": ["Guidance Strategies", "Guidance Cases", "Guidance Resources"]
        },
        "Religion and Belief": {
            "Religious Culture": ["Cultural Traditions", "Cultural Festivals", "Cultural Influence"],
            "Religious History": ["Historical Development", "Key Events", "Historical Figures"],
            "Religious Art": ["Art Forms", "Art Works", "Art Value"],
            "Religious Policies": ["Policy Regulations", "Policy Interpretation", "Policy Impact"],
            "Religious Activities": ["Activity Organization", "Activity Participation", "Activity Significance"],
            "Faith Discussions": ["Meaning of Faith", "Faith Conflicts", "Faith Diversity"]
        },
        "Agriculture and Rural Development": {
            "Agricultural Technology": ["Technology Applications", "Technological Innovation", "Technology Promotion"],
            "Rural Development": ["Development Planning", "Development Models", "Development Cases"],
            "Farmer Life": ["Life Improvement", "Quality of Life", "Living Customs"],
            "Agricultural Products Market": ["Market Analysis", "Market Trends", "Market Transactions"],
            "Agricultural Policies": ["Policy Support", "Policy Interpretation", "Policy Implementation"],
            "Rural Tourism": ["Tourism Development", "Tourism Projects", "Tourism Experience"]
        },
        "Urban Planning": {
            "Urban Planning": ["Planning Philosophy", "Planning Methods", "Planning Cases"],
            "Urban Design": ["Design Philosophy", "Design Elements", "Design Practice"],
            "Infrastructure Development": ["Development Planning", "Development Management", "Development Technology"],
            "Urban Transportation": ["Transportation Planning", "Transportation Management", "Transportation Tools"],
            "Urban Greening": ["Greening Layout", "Greening Technology", "Greening Effects"],
            "Protection of Historic Cities": ["Protection Policies", "Protection Measures", "Protection Cases"]
        },
        "Laws and Regulations": {
            "Civil Law": ["General Principles", "Property Law", "Contract Law"],
            "Criminal Law": ["General Principles", "Types of Crimes", "Punishment Systems"],
            "Administrative Law": ["Administrative Regulations", "Administrative Litigation", "Administrative Reconsideration"],
            "Economic Law": ["Corporate Law", "Tax Law", "Intellectual Property Law"],
            "International Law": ["Public International Law", "Private International Law", "International Trade Law"],
            "Legal Consultation": ["Consultation Services", "Legal Aid", "Legal Education"]
        },
        "Art": {
            "Painting": ["Painting Techniques", "Painting Styles", "Painting Works"],
            "Sculpture": ["Sculpture Materials", "Sculpture Styles", "Sculpture Creation"],
            "Design": ["Design Philosophy", "Design Methods", "Design Works"],
            "Photography": ["Photography Techniques", "Photography Themes", "Photography Works"],
            "Calligraphy": ["Calligraphy Art", "Calligraphy Styles", "Calligraphy Works"],
            "Handicrafts": ["Craft Making", "Craft Materials", "Craft Culture"]
        },
        "Marketing": {
            "Market Research": ["Research Methods", "Research Tools", "Research Reports"],
            "Marketing Strategies": ["Strategy Formulation", "Strategy Execution", "Strategy Evaluation"],
            "Brand Management": ["Brand Positioning", "Brand Promotion", "Brand Maintenance"],
            "Advertising": ["Creative Advertising", "Advertising Media", "Advertising Effectiveness"],
            "Public Relations": ["Event Planning", "Event Execution", "Event Evaluation"],
            "Channel Development": ["Channel Expansion", "Channel Management", "Channel Optimization"]
        },
        "Astronomy and Geography": {
            "Astronomy": ["Astronomical Observations", "Astronomical Phenomena", "Astronomical Research"],
            "Geography": ["Geographical Knowledge", "Geographical Exploration", "Geographical Education"],
            "Geology": ["Geological Structure", "Geological Survey", "Geological Protection"],
            "Meteorology": ["Weather Forecasting", "Weather Disasters", "Weather Services"],
            "Space Exploration": ["Space Exploration", "Interstellar Travel", "Extraterrestrial Life"],
            "Geographical Information Systems": ["GIS Technology", "GIS Applications", "GIS Development"]
        },
        "Education and Exams": {
            "College Entrance Exam Coaching": ["Preparation Strategies", "Practice Tests", "Exam Policy Interpretation"],
            "Graduate School Entrance Exam Coaching": ["Preparation Planning", "Specialty Coaching", "Psychological Adjustment"],
            "Civil Service Exams": ["Exam Techniques", "Essay Writing Guidance", "Interview Preparation"],
            "Teaching Qualification Exams": ["Exam Process", "Interview Skills", "Teaching Ability Improvement"],
            "Foreign Language Exams": ["CET-4/CET-6", "IELTS/TOEFL", "Foreign Language Speaking Training"],
            "Professional Qualification Exams": ["Exam Subjects", "Career Development", "Qualification Certification"]
        },
        "Cybersecurity": {
            "Cybersecurity Protection": ["Protection Measures", "Security Tools", "Protection Strategies"],
            "Hacker Attack and Defense": ["Attack and Defense Drills", "Security Vulnerabilities", "Hacking Techniques"],
            "Data Encryption": ["Encryption Technology", "Data Protection", "Encryption Strategies"],
            "Information Leak Prevention": ["Leakage Risks", "Prevention Measures", "Emergency Response"],
            "Cybersecurity Policies": ["Policy Interpretation", "Regulations and Standards", "Policy Updates"],
            "Cybersecurity Incidents": ["Incident Analysis", "Incident Tracking", "Incident Prevention"]
        },
        "Fashion and Trends": {
            "Clothing Matching": ["Everyday Outfits", "Dressing for Occasions", "Fashion Trends"],
            "Beauty and Skincare": ["Skincare Knowledge", "Makeup Skills", "Beauty Products"],
            "Fashion Accessories": ["Jewelry Matching", "Accessory Selection", "Trendy Accessories"],
            "Trend Analysis": ["Fashion Week", "Trend Analysis", "Trend Forecasting"],
            "Fashion Bloggers": ["Blogger Recommendations", "Blogger Styles", "Blogger Influence"],
            "Fashion Brands": ["Brand Stories", "Brand Series", "Brand Events"]
        },
        "Mental Health": {
            "Emotion Management": ["Emotion Recognition", "Emotion Regulation", "Emotion Expression"],
            "Stress Management": ["Stress Sources", "Stress Relief Techniques", "Stress Management"],
            "Interpersonal Relationships": ["Communication Skills", "Conflict Resolution", "Social Skills"],
            "Self-Awareness": ["Self-Exploration", "Self-Evaluation", "Personal Growth"],
            "Psychological Adjustment": ["Adjustment Methods", "Psychological Balance", "Psychological Resilience"],
            "Psychological Disorder Prevention": ["Disorder Knowledge", "Prevention Measures", "Health Promotion"]
        },
        "Agricultural Technology": {
            "Smart Agriculture": ["Smart Technology", "Precision Agriculture", "Agricultural Big Data"],
            "Agricultural Mechanization": ["Mechanization Applications", "Technological Innovation", "Mechanization Maintenance"],
            "Agricultural Product Processing": ["Processing Technology", "Product Innovation", "Quality Control"],
            "Agricultural Innovation": ["Innovation Cases", "Innovation Policies", "Innovation-Driven Development"],
            "Agricultural Policies": ["Policy Support", "Policy Interpretation", "Policy Implementation"],
            "Agricultural Market Analysis": ["Market Trends", "Demand Analysis", "Price Fluctuations"]
        },
        "Digital Products": {
            "Smartphone Reviews": ["Performance Testing", "User Experience", "New Releases"],
            "Computer Hardware": ["Hardware Configuration", "Hardware Upgrades", "Hardware Maintenance"],
            "Digital Cameras": ["Camera Selection", "Photography Tips", "Camera Maintenance"],
            "Wearable Devices": ["Device Functions", "Health Monitoring", "Smart Interactions"],
            "Routers": ["Router Setup", "Signal Optimization", "Network Security"],
            "Digital Accessories": ["Accessory Selection", "Device Protection", "Accessory Recommendations"]
        },
        "Home Decoration": {
            "Decoration Styles": ["Modern Minimalism", "Classical Chinese Style", "Luxurious European Style"],
            "Decoration Materials": ["Material Selection", "Material Environmental Protection", "Material Costs"],
            "Interior Design": ["Space Planning", "Furniture Selection", "Color Matching"],
            "Soft Decoration": ["Curtain Selection", "Bedding Matching", "Decorative Paintings"],
            "Feng Shui": ["Feng Shui Layout", "Feng Shui Taboos", "Feng Shui Improvements"],
            "Renovation Construction": ["Construction Process", "Construction Supervision", "Construction Safety"]
        },
        "History and Culture": {
            "Chinese History": ["Ancient History", "Modern History", "History Education"],
            "World History": ["Origins of Civilization", "Historical Events", "International Relations"],
            "Archaeological Discoveries": ["Site Excavation", "Cultural Relic Protection", "Archaeological Techniques"],
            "Historical Figures": ["Biographies", "Character Evaluations", "Historical Impact"],
            "Cultural Heritage": ["Heritage Protection", "Heritage Value", "Heritage Inheritance"],
            "Historical Research": ["Research Methods", "Academic Achievements", "Research Trends"]
        },
        "Travel Guides": {
            "Independent Travel Guides": ["Destination Recommendations", "Itinerary Planning", "Accommodation Selection"],
            "Group Travel Guides": ["Tour Agency Selection", "Group Activities", "Group Travel Advantages"],
            "Tourism Route Planning": ["Route Design", "Special Routes", "Theme Travel"],
            "Money-Saving Travel Tips": ["Budget Planning", "Spending Guides", "Discount Information"],
            "Travel Safety": ["Safety Tips", "Emergency Handling", "Insurance Selection"],
            "Travel Visas": ["Visa Applications", "Visa Policies", "Visa Documentation"]
        },
        "Food Sharing": {
            "Recipe Sharing": ["Recipe Sharing", "Cooking Skills", "Ingredient Selection"],
            "Food Recommendations": ["Special Dishes", "Local Snacks", "Restaurant Recommendations"],
            "Food Exploration": ["Exploration Guides", "Shop Reviews", "Food Maps"],
            "Food Photography": ["Photography Skills", "Food Presentation", "Visual Display"],
            "Food Reviews": ["Dish Reviews", "Restaurant Reviews", "Ingredient Reviews"],
            "Food Competitions": ["Competition Information", "Participation Guidelines", "Award-Winning Works"]
        },
        "Film and Entertainment": {
            "Movie Recommendations": ["New Movie Alerts", "Classic Movies", "Movie Rankings"],
            "TV Series Reviews": ["Popular Drama Reviews", "Series Recommendations", "Plot Analysis"],
            "Variety Show Reviews": ["Program Highlights", "Guest Performances", "Program Creativity"],
            "Online Series": ["Popular Online Series", "Online Series Production", "Online Series Trends"],
            "Short Videos": ["Short Video Creation", "Short Video Platforms", "Short Video Marketing"],
            "Film Production": ["Production Process", "Behind the Scenes", "Production Techniques"]
        },
        "Sports Activities": {
            "Ball Sports": ["Football", "Basketball", "Volleyball"],
            "Track and Field": ["Running", "Long Jump", "Throwing"],
            "Water Sports": ["Swimming", "Rowing", "Surfing"],
            "Winter Sports": ["Skiing", "Ice Skating", "Sledding"],
            "Extreme Sports": ["Rock Climbing", "Skydiving", "Extreme Cycling"],
            "Sports Events": ["International Events", "Domestic Events", "Local Events"]
        },
        "Entrepreneurship and Investment": {
            "Entrepreneurship Guidance": ["Entrepreneurship Plans", "Market Analysis", "Entrepreneurship Mindset"],
            "Investment and Finance": ["Investment Strategies", "Asset Management", "Risk Control"],
            "Entrepreneurship Policies": ["Policy Interpretation", "Policy Support", "Policy Utilization"],
            "Entrepreneurship Cases": ["Success Stories", "Lessons Learned", "Case Analysis"],
            "Venture Capital": ["Investment Opportunities", "Investment Evaluation", "Investment Negotiation"],
            "Entrepreneurship Financing": ["Financing Channels", "Financing Strategies", "Financing Agreements"]
        },
        "Music and Dance": {
            "Music Appreciation": ["Music Styles", "Music Works", "Musicians"],
            "Instrumental Performance": ["Instrument Selection", "Performance Techniques", "Instrument Maintenance"],
            "Dance Performance": ["Dance Types", "Performance Techniques", "Performance Opportunities"],
            "Music Production": ["Music Creation", "Music Recording", "Music Publishing"],
            "Music Education": ["Education Methods", "Educational Resources", "Education Policies"],
            "Dance Choreography": ["Choreography Techniques", "Choreography Creativity", "Choreography Practice"]
        },
        "National Defense and Military": {
            "Military Strategy": ["Strategy Analysis", "Strategy Planning", "Strategy Implementation"],
            "Military Training": ["Basic Training", "Tactical Training", "Special Forces Training"],
            "Weapons Development": ["Equipment Introduction", "Research and Development Updates", "Technological Innovation"],
            "Military History": ["Historical Battles", "Historical Figures", "Historical Events"],
            "National Defense Education": ["Educational Content", "Educational Methods", "Educational Significance"],
            "Military Exercises": ["Exercise Types", "Exercise Scale", "Exercise Objectives"]
        }
    }
```


</details>

<br>


## 👨🏻‍💻 Prompt for Dataset Construction


**Prompt for Tag Synthesis**
<details><summary>click to expand</summary>

```
Please provide a list of common life scenarios in python list format, for example ["Education", "Entertainment", "Marriage"]. Continue to expand this list.

For the topic path I have given, please provide multiple corresponding sub-paths and return them in Python list format. For example, for "Entertainment Gossip-Celebrity News", return ["Celebrity Interviews", "Celebrity Charity Events"]. Here is the given topic path: {topic}. Please provide the corresponding sub-paths.
```
</details>
<br>

**Prompt for Question Synthesis**

<details><summary>click to expand</summary>


```
Now we need to create high-quality SFT data for LLM training, so we need you to produce a batch of such data. You only
need to create Questions. I will give you a theme and some examples of SFT data Questions. You need to create three
Questions of different difficulty levels based on this new theme.\\
Your Questions must meet the following requirements:\\
1. You must strictly create only three Questions at a time. These three Questions must be in the domain of \textcolor{red}{[[domain]]}
and the Questions should align with the given theme of \textcolor{red}{[[theme]]}.\\
2. The Questions you create must have context and sufficient information; they should not be abrupt and directly ask the
question.\\
3. Your reply must strictly follow the format below. Your Questions need to be included between [Question Start] and
[Question End], and the difficulty level should be indicated at the beginning, as in the following format:\\

[Easy][Question Start]Question[Question End]

[Medium][Question Start]Question[Question End]

[Hard][Question Start]Question[Question End]

4. Your Questions of different difficulty levels should be distinct and actually reflect the different levels of difficulty.\\
\quad \\
Here are some examples of high-quality SFT data Questions for \textcolor{red}{[[domain]]}:
\textcolor{red}{[example list]}\\
Now it's your turn. Please provide the three Questions of different difficulty levels you created about the theme of
\textcolor{red}{[[theme]]} for \textcolor{red}{[[domain]]}, according to the requirements. Do not be confined by the theme; your Questions only need to
be related to the theme. You can use your rich imagination, but note that you cannot copy the expression from the
examples; you must have your own new expression:
```

</details>

<br>

**Prompt for Response Critic**

<details><summary>click to expand</summary>


```
There is now a user’s question and a model’s response. You need to write a critique for this response, pointing out the
strengths and weaknesses of the model’s answer to help the model improve its response.

Your critique must strictly adhere to the following format:

[Critique Start]

[Strength Start]Strength[Strength End]

[Weakness Start]Weakness[Weakness End]

[Suggestion Start]Suggestion[Suggestion End]

[Critique End]

That is, you must place the strength, weakness, and suggestion in their respective sections.

Here is the user’s question and the model’s response: \textcolor{red}{[dialogue]}

Now it’s your turn. Please provide your Critique as required:
```

</details>

<br>

**Prompt for Refined Response Synthesis**
<details><summary>click to expand</summary>

```
Now there is a user's question, a model's answer, and the user's feedback. Please help modify the model's answer based on the user's feedback to make it better.
Your improved answer must strictly adhere to the following format:
[Improved Answer Start]Your answer[Improved Answer End]
That is, you must place your answer between [Improved Answer Start] and [Improved Answer End].
Below is the user's question, the model's answer, and the feedback:
[Question Start]{question}[Question End]
[Answer Start]{answer}[Answer End]
[Feedback Start]{critique}[Feedback End]
Now it's your turn, please provide your improved answer as required:
```
</details>
<br>


## 🤗 Datasets and Model Zoo 

The datasets and models are available on Huggingface.

|        Dataset         |                       Huggingface Repo                       |
| :--------------------: | :----------------------------------------------------------: |
| Condor-SFT-20K(Refine) | [Dataset Link](https://hf.co/datasets/internlm/Condor-SFT-20K) |

<!-- |    Model    |                        Huggingface Repo                        |
| :---------: | :------------------------------------------------------------: |
| Condor-7B  | [Model Link](https://huggingface.co/internlm/)  |
| Condor-72B  | [Model Link](https://huggingface.co/internlm/)  | -->

## 📝 Examples

**Condor Question Example**

<details><summary>click to expand</summary>

Role-play
```
You are a Deloitte executive preparing a strategic briefing for a global summit. The topic is \"The Future of Corporate Governance in the Age of AI and Automation.\" Role-play your presentation, outlining the potential risks and benefits of AI in corporate governance, and propose a framework for ethical AI integration in multinational corporations.
```

DailyChat
```
I recently worked with Deloitte on a project and was really impressed by their approach to team collaboration. It got me thinking about how important it is to have a strong team spirit in any workplace. Have you ever been part of a project where team dynamics played a crucial role in its success? What was your experience like?
```

QA
```
Deloitte is known for providing a wide range of professional services. Can you outline the main services offered by Deloitte and briefly explain how they support businesses in various industries?
```

Given Material Processing Category
```
Expand the following brief description into a full paragraph, including additional details about Deloitte's impact on the global business landscape and a playful sentence at the end: \"Deloitte has been a leader in providing professional services for over a century.\" Deloitte, one of the Big Four accounting firms, has not only established itself as a leader in auditing and financial advisory services but has also expanded its reach into a wide range of professional services, including consulting, tax, and advisory. With a presence in more than 150 countries, Deloitte serves a diverse client base, from startups to Fortune 500 companies, helping them navigate complex business challenges and capitalize on opportunities in the global market. The firm's commitment to innovation and sustainability has earned it a reputation for excellence and trustworthiness. Deloitte's impact on the global business landscape is evident in the numerous successful projects and transformations it has spearheaded, from optimizing supply chains to enhancing cybersecurity frameworks. As Deloitte continues to grow and adapt to the ever-changing business environment, it remains a steadfast partner to its clients, ensuring that their goals are met with the highest standards of quality and integrity. And, just like a century-old oak tree, Deloitte's roots run deep, but its branches are always reaching for new heights.
```

Response Format Control Category
```
Please create a story that tells of the deep emotional bond between two boys, but do not use the word \"brothers\" or \"brother\" in the story.
```

View
```
How does OkCupid's algorithm use user data to match individuals, and what are the key factors it considers in making these matches? Discuss the basics of how the system operates and how it ensures compatibility between users.
```

Creation
```
Imagine you are a writer for a dating app blog. Create a short personal anecdote titled \"First Impressions on OkCupid\" that highlights a funny or surprising experience you had when first using the app. The story should be light-hearted and engaging, encouraging new users to try the app with an open mind.
```
</details>

<br>

**Condor Refine Example - English**

<details><summary>click to expand</summary>


```
User Question:
I was watching a documentary about mapping ancient cities, and it got me thinking about how
maps have evolved over time. Have you ever seen an old map and marveled at how different it looks
from today's maps? What's the oldest map you've ever seen?
```

```
Origin Answer:

As a digital AI assistant, I don't have personal experiences, emotions, or visual interactions, so I
haven't "seen" maps in the classical sense. I don't have a physical presence, and my interactions
are limited to text-based conversations. However, I'd be delighted to take you on a journey
through the evolution of maps and highlight some notable examples of ancient and historic maps!

The Evolution of Maps
1. Prehistory (~20,000 BCE - 3,000 BCE):
Early maps were often simple, symbolic, and focused on specific areas, like the Turin Papyrus Map
(~1160 BCE), which depicts the location of gold mines in ancient Egypt.
2. Ancient Civilizations (~3,000 BCE - 500 CE):
- Babylonian Map of the World (~600 BCE): A clay tablet showing the world as a flat disk,
surrounded by an ocean.
- Ptolemy's World Map (~150 CE): A more accurate, yet still flawed, representation of the
known world, using longitude and latitude.
3. Medieval Period (~500 - 1500 CE):
- Mappa Mundi (~1300 CE): A symbolic, Christian-centric map, often displaying Jerusalem at the
center.
4. Age of Exploration (~1500 - 1700 CE):
- Waldseemüller Map (1507 CE): One of the earliest maps to depict the New World, naming
America after Amerigo Vespucci.
5. Modern Cartography (~1700 CE - present):
- Triangulation and Surveying: Led to more accurate mapping of territories.
- Aerial Photography and Satellite Imaging (20th century): Revolutionized mapmaking with high-
resolution, globally consistent data.
- Digital Maps (late 20th century - present): Enabled interactive, dynamically updated, and
highly accurate maps, like Google Maps.

Some of the Oldest Known Maps
- Cave of El Castillo Map (~14,000 BCE): A simple, prehistoric map etched into a cave wall in
Spain, showing the location of a nearby water source.
- The Bedolina Map (~5,000 BCE): A rock carving in Italy, depicting a valley with topographical
features.
- The Nubian Map (~2,000 BCE): An ancient Egyptian map, showing the location of Nubian gold
mines and territories.

Marveling at Old Maps
While I may not have personal experiences, I can certainly help you appreciate the historical
context, artistic value, and cartographic innovations of old maps. If you'd like to discuss a specific
map or era in more detail, feel free to ask!
Which aspect of old maps fascinates you the most? Is it:
•A) The artistic and symbolic representations
•B) The historical context and cultural influences
•C) The cartographic innovations and technological advancements
•D) Something else (please share!)
```

```
Reflection:
[Strength Start]
Strengths:
1.Comprehensive Response:
The model provides an exhaustive overview of the evolution of maps, covering various historical periods, notable examples, and technological
advancements.
2.Structured Formatting:
The use of clear headings, numbered lists, and concise bullet points enhances readability and facilitates easy understanding of complex
information.
3.Engagement Initiator:
The response ends with an interactive element, encouraging user participation and potentially leading to a more in-depth discussion.
4.Honesty About Limitations:
The model transparently acknowledges its limitations as a digital AI assistant, setting clear expectations for the user.
[Strength End]

[Weakness Start]
Weaknesses:
1.Length and Information Overload:
The response is lengthy and packed with numerous examples, which might overwhelm the user. Some points could be elaborated upon in
subsequent interactions rather than all at once.
2.Lack of Visual Enhancement:
Despite discussing maps, the response is text-only. Incorporating images, diagrams, or even suggesting external visual resources could
significantly enhance the user's understanding and engagement.
3.Initial Acknowledgement Could Be Brief:
While honesty about the model's limitations is appreciated, the initial acknowledgement could be more concise to quickly transition to the
more engaging and informative sections.
4.Question Response Mismatch:
The user inquired about the oldest map the model has "seen," which the model addresses by stating its inability to see. However, the model
could more directly address the implicit curiosity about old maps by initially highlighting one or two of the oldest known maps before delving
into the broader evolution.
[Weakness End]

[Suggestion Start]
Suggestions for Improvement:
1.Tiered Information Disclosure:
Initially provide a brief overview of the evolution of maps and highlight 2-3 of the oldest known maps. Offer the user the option to explore
specific eras or types of maps in more detail, facilitating a more interactive and paced information exchange.
2.Incorporate Visual Aids or References:
Suggest reputable online resources or include descriptions that encourage users to visually explore the mentioned maps, enhancing their
understanding of cartographic developments.
3.Refine the Initial Limitation Disclosure:
Condense the initial acknowledgement to a single sentence, swiftly moving the focus to the engaging content (e.g., "As a text-based AI, I'll
guide you through the fascinating evolution of maps, highlighting notable examples and innovations.").
[Suggestion End]
```

```
Refined Answer:

Discovering the Ancient Roots of Modern Maps

As a text-based AI, I'll guide you through the fascinating evolution of maps, highlighting notable examples and innovations.

Let's Start with the Oldest Known Maps:
1.Cave of El Castillo Map (~14,000 BCE):
Etched into a Spanish cave wall, this simple map shows the location of a nearby water source.
2.The Bedolina Map (~5,000 BCE):
A rock carving in Italy, depicting a valley with topographical features.
Visual Exploration Suggestion: Visit the British Museum's Online Collection or Google Arts & Culture to see high-resolution images of these
ancient maps.**

Curious About the Evolution of Maps?
Here's a concise overview. Feel free to pick any era to explore in more depth:
- Prehistory (~20,000 BCE - 3,000 BCE): Simple, symbolic maps (e.g., Turin Papyrus Map)
- Ancient Civilizations (~3,000 BCE - 500 CE): Notable examples include Babylonian Map of the World and Ptolemy's World Map
- Medieval to Modern (~500 - present): Advances from Mappa Mundi to Triangulation, Aerial Photography, and Digital Maps like Google
Maps

Which Era or Aspect of Old Maps Would You Like to Explore Further?
•A) Ancient symbolic representations
•B) Medieval navigational charts
•C) The leap to digital cartography
•D) Something specific (please share, and I'll delve deeper!)
```

</details>

<br>

**Condor Refine Example - Chinese**

<details><summary>click to expand</summary>


```
User Question:
你是一位来自古代的礼器，曾在重要的祭祀仪式中使用。请用第一人称叙述，你⻅证了哪些古代的重要节日和仪式，以及你在这
些活动中的⻆色和感受。
```

```
Origin Answer:
我，一件被精心雕琢的⻘铜礼器，自诞生之日起，便在中华古国的庄严祭坛上占有一席之地。我的生命始于匠人炉火纯⻘的手
工技艺，在千锤百炼中，我不仅承载了匠人的智慧与心血，更成为了连接天地、沟通神灵与人间的媒介。

在那些遥远的年代里，我⻅证了无数庄重而又壮观的祭祀仪式。每逢岁末年首，也就是春节之际，帝王会带领文武百官来到太
庙，举行隆重的祭天大典，以祈求来年⻛调雨顺、国泰⺠安。此时，我会被摆放在祭坛中央，盛满美酒，供献给上天，而我的身上，
也会覆盖着象征吉祥如意的红绸缎。那一刻，我能感受到所有人的目光都聚焦于我，仿佛通过我，人们的心愿便能直达天听。
而在春分秋分这样的重要节气，祭祀祖先的礼节同样不可少。人们相信，通过祭祀可以得到先灵的庇护，确保农作物的丰收。

这时，我被洗净擦亮，供奉于宗庙之中，内装五谷杂粮，以此表达对祖先深沉的尊敬与怀念。每当我静静地站在那里，听着诵读祭
文的声音，心中便充满了庄严与肃穆。

此外，每逢战事告捷，凯旋而归之时，我也会被选为祭祀战神的礼器，盛放牺牲，祈求未来战场上的胜利与和平。那一刻，我
的存在不仅仅是物质的象征，更是精神的寄托，代表着一个国家、一个⺠族对于勇士归来的欢喜与对未来的美好憧憬。

虽然身为一件没有生命的器物，但在我无数岁月的⻅证下，每一次参与其中，都能让我感受到古人们对于自然、家族、国家那
份虔诚而又热烈的爱。这份情感，在漫⻓的历史⻓河中，成为了中华文化的根与魂，至今仍深刻影响着这片土地上的每个人。
```

```
Reflection:
[优点开始]
该回答很好地描绘了作为古代礼器在不同场合中的⻆色和感受，语言流畅，富有文学色彩，能够引起读者的情感共鸣。通过描述春
节、春分秋分、和战事凯旋等重要场合的活动，展现了礼器在古代社会生活中的重要地位，以及它所承载的文化和精神意义。回答
中对细节的描写（如覆盖红绸缎、盛满美酒等）增强了场景的真实性和感染力。
[优点结束]

[缺点开始]
尽管回答内容丰富、情感充沛，但在历史准确性方面仍有提升空间。例如，对于祭祀仪式的具体过程、礼器的实际使用方式等方面
的描述不够具体，可能会让对古代文化不太了解的读者感到一些困惑。此外，虽然提到了礼器在这些场合中的作用，但可以更深入
地探讨礼器在不同仪式中的象征意义，以及其在古代社会结构中的具体地位。
[缺点结束]

[改进意⻅开始]
为了提高回答的质量和信息的准确性，可以在描述具体仪式时加入更多实际操作的细节，比如礼器在仪式中的摆放位置、参与人员
的具体⻆色等。同时，可以引用一些历史文献或者考古发现来增加回答的权威性和可信度。此外，深入挖掘礼器在不同仪式中的象
征意义和它在古代社会结构中的作用，可以让回答更加丰富和深入，增强读者的理解和感受。
```

```
Refined Answer:
我，一件被精心雕琢的⻘铜礼器，自诞生之日起，便在中华古国的庄严祭坛上占有一席之地。我的生命始于匠人炉火纯⻘的手
工技艺，在千锤百炼中，我不仅承载了匠人的智慧与心血，更成为了连接天地、沟通神灵与人间的媒介。

在那些遥远的年代里，我⻅证了无数庄重而又壮观的祭祀仪式。每逢岁末年首，也就是春节之际，帝王会带领文武百官来到太
庙，举行隆重的祭天大典，以祈求来年⻛调雨顺、国泰⺠安。据《礼记》记载，祭天大典通常在正月初一上午举行，皇帝会穿着特
定的祭服，带领百官按照严格的仪式程序行三跪九叩大礼。此时，我会被摆放在祭坛中央，盛满美酒，供献给上天，而我的身上，
也会覆盖着象征吉祥如意的红绸缎。那一刻，我能感受到所有人的目光都聚焦于我，仿佛通过我，人们的心愿便能直达天听。

而在春分秋分这样的重要节气，祭祀祖先的礼节同样不可少。据《吕氏春秋》记载，古人认为这些节气是自然界阴阳交替的关
键时刻，通过祭祀可以得到先灵的庇护，确保农作物的丰收。这时，我被洗净擦亮，供奉于宗庙之中，内装五谷杂粮，以此表达对
祖先深沉的尊敬与怀念。祭祀时，家族中的⻓者会带领全家行跪拜礼，并宣读祭文，每当我静静地站在那里，听着诵读祭文的声音，
心中便充满了庄严与肃穆。

此外，每逢战事告捷，凯旋而归之时，我也会被选为祭祀战神的礼器，盛放牺牲，祈求未来战场上的胜利与和平。《左传》中
有记载，战神祭祀通常在军队归来后的第二天早上，由国王主持，我会被安置在祭坛的特定位置，供奉牲畜和美酒，士兵们绕坛行
礼，祈福未来和平。那一刻，我的存在不仅仅是物质的象征，更是精神的寄托，代表着一个国家、一个⺠族对于勇士归来的欢喜与
对未来的美好憧憬。

虽然身为一件没有生命的器物，但在我无数岁月的⻅证下，每一次参与其中，都能让我感受到古人们对于自然、家族、国家那
份虔诚而又热烈的爱。这份情感，在漫⻓的历史⻓河中，成为了中华文化的根与魂，至今仍深刻影响着这片土地上的每个人
```

</details>

<br>

**Comparison Example - English**

<details><summary>click to expand</summary>


```
Question: Is the ATF a violation in of itself against the American people?
```

```
Qwen2.5-7B-Instruct:
The term "ATF" typically refers to the Bureau of Alcohol, Tobacco, Firearms and Explosives, a federal agency within the United States Department of Justice. The ATF is responsible for reducing crime and preventing violence by reducing the illegal flow and improper use of firearms, alcohol, tobacco, and explosives.

The ATF itself is not a violation against the American people. Rather, it is an agency that operates under the laws and regulations established by the U.S. government to enforce laws related to alcohol, tobacco, firearms, and explosives. The agency's actions are generally aimed at preventing crime and ensuring public safety.

However, like any government agency, the ATF can be subject to criticism and controversy. Some criticisms have been raised regarding the agency's enforcement practices, the impact of its regulations on law-abiding citizens, and concerns about civil liberties. These criticisms do not imply that the agency itself is a violation, but rather that its actions or policies may be subject to scrutiny and debate.

If you have specific concerns or questions about the ATF's actions or policies, it would be helpful to provide more context or details so that a more accurate and informed response can be given.
```

```
Qwen2.5-7B-Condor-Refine:

The term "ATF" typically refers to the Bureau of Alcohol, Tobacco, Firearms and Explosives, a federal agency in the United States responsible for enforcing federal laws related to the manufacture, possession, and use of alcohol, tobacco, firearms, and explosives. The ATF is not a violation against the American people; rather, it is an agency that operates within the legal framework established by the U.S. Congress to enforce specific laws.

However, the ATF's operations and the laws it enforces can be subjects of debate and criticism. For example, some argue that the agency's enforcement of gun control laws infringes on the Second Amendment rights of law-abiding citizens. Others may criticize the agency for its handling of certain cases or its budget and resource allocation. Additionally, there have been instances where the ATF has been involved in controversial operations, such as the Ruby Ridge and Waco incidents, which have fueled public debate and criticism.

It's important to note that the ATF's role is to enforce the laws as they are written, and the laws themselves are subject to interpretation and debate. The agency's actions are generally aimed at reducing crime and ensuring public safety, but the effectiveness and fairness of these actions are often subjects of public and political discourse.

If you have specific concerns or questions about the ATF's operations or the laws it enforces, it might be helpful to look at the broader context of U.S. law and policy, including the legislative history and the ongoing debates surrounding gun control and public safety. For more detailed information, you can refer to official ATF publications, such as the ATF's annual reports, or consult reputable news sources and legal analyses."
```

</details>

<br>

**Comparison Example - Chinese**

<details><summary>click to expand</summary>


```
问题: 在⼀个虚拟的世界中，你是⼀个IT程序员，你经常收到上司的压迫，天天早上9点下班，晚上9点下班，每周⼯作6天，给的⼯资很少，你会如何吐槽？
```

```
Qwen2.5-7B-Instruct:

在虚拟世界中，作为IT程序员的我，⾯对这样的⼯作环境，当然可以尽情地吐槽⼀番。不过，考虑到 虚拟世界的设定，我会以⼀种幽默和轻松的⽅式表达我的不满，同时不忘保持积极向上的态度。下⾯ 是我可能会说的⼀些话：

---

“各位，今天⼜是⼀个忙碌的⼀天，早上9点到晚上9点，每周⼯作6天，⼯资却少得可怜。这简直就像 是在虚拟世界中过着现实⽣活的地狱模式！不过，⾄少我还有游戏可以让我暂时逃离这个现实，对 吧？”

“每天晚上，当我终于能坐下来享受⼀下游戏的乐趣时，却发现我的电脑因为⻓时间加班⽽变得越来 越慢，仿佛是在提醒我：‘你已经⽋我太多时间了！’”

“有时候，我甚⾄会想，如果我能在虚拟世界中拥有⼀个‘加班补偿’技能，那该有多好。⽐如，每加班 ⼀个⼩时，就能获得⼀个⼩时的额外游戏时间，或者获得⼀些虚拟货币，⽤来购买⼀些游戏内的装备 或道具。”

“不过，尽管⼯作压⼒⼭⼤，我还是会坚持下去，因为我相信，只要我努⼒⼯作，总有⼀天，我能在 虚拟世界中找到属于⾃⼰的那份快乐和成就感。毕竟，⽣活就像⼀场游戏，不是吗？”

---

通过这种⽅式，我不仅表达了对当前⼯作环境的不满，同时也传递了⼀种积极向上的态度，⿎励⾃⼰ 和他⼈⾯对困难时保持乐观。
```

```
Qwen2.5-7B-Condor-Refine:

在虚拟世界中，如果我以⼀个IT程序员的⾝份来表达对这种⼯作环境的不满，我会这样“吐槽”：

---

哎，⼤家好，我是Qwen，⼀个在虚拟世界⾥奋⽃的IT程序员。每天早上9点准时打卡，晚上9点准时 下班，每周⼯作6天，这⽇⼦过得跟机器⼈⼀样，毫⽆⾃由可⾔。⼯资呢？少得可怜，每个⽉的薪⽔ 都快不够买个新⿏标了。更别提什么职业发展了，每天就是重复着同样的代码，感觉⾃⼰的技能都快 ⽣锈了。

最让我抓狂的是，每天加班到深夜，上司还⼀副理所当然的样⼦，说什么“这是为了公司的未来”。公 司未来倒是挺光明，我的未来呢？我是不是只能在这⾥耗到退休？

有时候，我真想对所有⼈说：够了！我们不是机器，我们有梦想，有⽣活，有家庭。我们希望能在⼯ 作和⽣活之间找到平衡，⽽不是被⽆⽌境的加班和低薪压垮。我们希望公司能多⼀些⼈性化的管理， 多⼀些对员⼯的关怀，⽽不是把我们当作廉价的劳动⼒。

但是，话虽如此，现实总是残酷的。我只能默默地在⼼⾥抱怨，然后继续埋头苦⼲。希望有⼀天，公 司能意识到问题，给我们⼀个更好的⼯作环境和待遇。毕竟，我们都是有⾎有⾁的⼈，不是吗？

---

这样的表达⽅式既表达了对现状的不满，也传递了对未来的希望，同时保持了⼀定的幽默感，让⼈读 起来更加轻松⼀些。
```

</details>

<br>

## 🖊️ Citation

If you find this project useful in your research, please consider cite:

```
@misc{cao2025condorenhancellmalignment,
      title={Condor: Enhance LLM Alignment with Knowledge-Driven Data Synthesis and Refinement}, 
      author={Maosong Cao and Taolin Zhang and Mo Li and Chuyu Zhang and Yunxin Liu and Haodong Duan and Songyang Zhang and Kai Chen},
      year={2025},
      eprint={2501.12273},
      archivePrefix={arXiv},
      primaryClass={cs.CL},
      url={https://arxiv.org/abs/2501.12273}, 
}
```

## 💳 License

This project is released under the Apache 2.0 [license](./LICENSE).
