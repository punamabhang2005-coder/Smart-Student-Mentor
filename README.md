# Smart Student Monitor

## Project Description
Smart Student Monitor is an AI-powered platform that helps teachers monitor student performance and provides personalized feedback to improve learning.

## Problem Statement
Teachers find it difficult to monitor every student's academic progress and provide individual guidance. This system helps automate student performance analysis and mentor support.

## Objectives
- Monitor student academic performance.
- Analyze essays using AI.
- Provide personalized mentor feedback.
- Track student growth over time.

## Team Members
- Punam Abhang
- Akash Chavhan
- Sarthak Thakare

## Technologies
- React
- FastAPI
- Python
- MySQL
- Machine Learning

## Project Modules
- Frontend
- Backend
- AI Module
- Database
- Documentation

## Repository Structure
- frontend/
- backend/
- ai/
- database/
- data/
- docs/
- test/

## Project Status
Project planning and documentation phase.
Implementation will begin after system design is finalized.








1.	imagine we have 50 essay data points at a time how are going to use that data in your project.
   
This is where our project becomes intelligent. The 50 essays are not just stored—they become the student's learning history. Every new essay is evaluated using those previous 50 essays.
Step 1: Build a Knowledge Profile from 50 Essays
Suppose Student A has written 50 essays.
Instead of storing only the text, the backend extracts features from each essay.
Essay	Grammar	Vocabulary	Critical Thinking	Creativity	Emotion	Overall
1	62	58	55	60	Positive	59
2	65	61	58	63	Positive	62
...	...	...	...	...	...	...
50	89	87	91	88	Confident	89
After 50 essays, the system knows the student's writing pattern.
Student Profile

Average Grammar = 82

Average Vocabulary = 80

Average Critical Thinking = 85

Average Creativity = 78

Average Essay Length = 720 words

Favorite Topics = AI, Education, Environment

Weak Area = Supporting arguments

Strong Area = Logical reasoning
This profile is updated after every submission.
________________________________________
Step 2: Convert Every Essay into AI Features
The raw essay is converted into structured data.
Example:
{
  "essay_id": 51,
  "grammar": 90,
  "vocabulary": 86,
  "critical_thinking": 92,
  "creativity": 88,
  "emotion": "Confident",
  "readability": 84,
  "word_count": 780,
  "embedding": [0.21, -0.34, 0.77, ...]
}
Notice the embedding. This is a numerical representation of the essay's meaning, allowing the AI to compare essays semantically, not just by keywords.
________________________________________
Step 3: Compare the New Essay with the Previous 50
When Essay #51 is submitted, the backend compares it with the student's history.
Instead of asking:
"Is this essay good?"
The system asks:
•	Is grammar improving? 
•	Is vocabulary richer? 
•	Is critical thinking stronger? 
•	Is the student repeating the same ideas? 
•	Has writing style changed? 
•	Is confidence increasing? 
•	Is there continuous improvement? 
Example:
Metric	Previous Average	Current Essay	Result
Grammar	82	90	+8
Vocabulary	80	86	+6
Critical Thinking	85	92	+7
Creativity	78	88	+10
The AI concludes:
This essay is significantly better than the student's historical average.
________________________________________
Step 4: Compare with the Student's Best Essays
The system also identifies the student's top-performing essays.
For example:
Best Essays

Essay 12

Essay 28

Essay 41

Essay 50
Now compare Essay 51 against those.
If Essay 51 scores higher than all previous essays:
New Personal Best

Previous Best Score = 89

Current Score = 93

Improvement = +4
This motivates students by showing personal milestones.
________________________________________
Step 5: Detect Long-Term Trends
Using all 50 essays, the backend detects trends rather than isolated scores.
For example:
Grammar

60 → 65 → 68 → 72 → 78 → 84 → 90
This indicates steady improvement.
Or:
Critical Thinking

85 → 84 → 82 → 80 → 77 → 74
This signals a decline, prompting the mentor to intervene.
________________________________________
Step 6: Generate Personalized Feedback
Because the AI has access to 50 previous essays, it can provide personalized comments instead of generic advice.
Example:
Compared with your previous 50 essays:
•	Your grammar improved by 8%. 
•	You used 15% more advanced vocabulary. 
•	Your arguments are stronger than in your last five essays. 
•	However, your conclusions remain shorter than average. Focus on summarizing your ideas more effectively. 
________________________________________
Step 7: Predict Future Performance
With enough historical data, you can even predict future progress.
Example:
Last 12 essays


71

74

76

79

81

83

85

87

89

91

92

93
The AI recognizes an upward trend and estimates that the student is likely to reach around 95–96 in the next few months if the current improvement continues. This can help mentors identify both high-performing and struggling students early.
________________________________________
Backend Workflow Using 50 Essays
Student submits Essay #51
          │
          ▼
Store the new essay
          │
          ▼
Extract features
(Grammar, Vocabulary, Creativity, Critical Thinking, Embedding)
          │
          ▼
Retrieve previous 50 essays
          │
          ▼
Calculate historical averages
          │
          ▼
Compare with previous essays
          │
          ▼
Detect improvement or decline
          │
          ▼
Generate AI feedback
          │
          ▼
Update student profile
          │
          ▼
Update ranking and progress graphs
Algorithms and models involved
Instead of a single algorithm, use a pipeline where each component has a specific job:
1.	LanguageTool – Grammar and spelling detection. 
2.	Sentence Transformers (BERT embeddings) – Convert essays into vectors for semantic similarity and comparison. 
3.	Cosine Similarity – Measure how similar the new essay is to previous essays and detect repeated ideas. 
4.	Readability Algorithms – Flesch Reading Ease and Flesch-Kincaid Grade Level. 
5.	LLM – Evaluate critical thinking, creativity, coherence, and generate personalized feedback. 
6.	Time-series trend analysis – Track improvement across the 50 essays and identify long-term growth or decline. 
This approach is much more powerful than simply scoring one essay because the AI acts like a mentor that remembers the student's complete writing journey, making every evaluation personalized, explainable, and based on real historical progress.


2.exact what happens ,when new essay submit to backend what algo backend will use to generate the review.

For a production-quality Student Mentor System, the backend should not rely on a single algorithm. Instead, it should use a pipeline where each stage performs one specific task. This makes the review more accurate, explainable, and scalable.
Complete Backend Flow
Student writes Essay
        │
        ▼
Frontend sends POST request
        │
        ▼
Backend API receives essay
        │
        ▼
Store original essay in Database
        │
        ▼
Text Preprocessing
        │
        ▼
Feature Extraction
        │
        ▼
Grammar Analysis
        │
        ▼
Semantic Analysis
        │
        ▼
Historical Comparison
        │
        ▼
AI Evaluation
        │
        ▼
Generate Review
        │
        ▼
Save Results
        │
        ▼
Return Response to Frontend
________________________________________
Step 1: Essay Submission
The frontend sends:
{
   "studentId":101,
   "essay":"Artificial Intelligence is changing education...",
   "month":"August"
}
________________________________________
Step 2: Store the Original Essay
The backend first saves the raw essay.
Essay Table

Essay ID
Student ID
Essay Text
Submission Time
Word Count
Status
Nothing is evaluated yet.
________________________________________
Step 3: Text Preprocessing
Algorithms used:
•	Tokenization 
•	Sentence Segmentation 
•	Lemmatization 
•	Stop-word Removal (only for analysis) 
•	Part-of-Speech Tagging 
Libraries:
•	spaCy 
•	NLTK 
Example
Input
AI is changing education.
Output
["AI","change","education"]
________________________________________
Step 4: Feature Extraction
The backend extracts measurable features.
Example
Word Count = 734

Paragraphs = 8

Average Sentence Length = 18

Unique Words = 425

Vocabulary Diversity = 0.61

Passive Voice = 7%

Reading Level = Grade 10
These become numerical features.
________________________________________
Step 5: Grammar Checking
Algorithm
LanguageTool
Checks
•	Grammar 
•	Spelling 
•	Punctuation 
•	Subject-Verb Agreement 
•	Tense Consistency 
Output
Grammar Score = 91

Grammar Errors = 6

Spelling Errors = 1
________________________________________
Step 6: Readability
Algorithms
•	Flesch Reading Ease 
•	Flesch-Kincaid Grade Level 
•	Gunning Fog Index 
Example
Reading Ease

73

Easy to Read
________________________________________
Step 7: Semantic Embedding
This is the most important AI step.
Algorithm
Sentence-BERT
The essay is converted into a vector.
Essay

↓

Embedding

↓

[0.21
0.56
-0.18
0.73
...]
The vector captures the meaning of the essay.
________________________________________
Step 8: Compare with Previous Essays
Algorithm
Cosine Similarity
The backend loads the student's previous 50 essays.
Essay 51

↓

Embedding
Compare with
Essay 50

Essay 49

Essay 48

...

Essay 1
Example
Previous Essay	Similarity
Essay 50	0.92
Essay 49	0.88
Essay 48	0.75
Interpretation:
•	Very high similarity (e.g., >0.95) may indicate repeated ideas. 
•	Moderate similarity shows continuity in writing style. 
•	Lower similarity can indicate new thinking or a different topic. 
________________________________________
Step 9: Critical Thinking Evaluation
A large language model evaluates aspects that traditional algorithms cannot.
Prompt (conceptually):
Evaluate:

Argument quality

Evidence

Reasoning

Logic

Counterarguments

Originality

Give scores out of 10.
Possible response
{
 "argument":9,
 "reasoning":8,
 "logic":9,
 "criticalThinking":8.7
}
________________________________________
Step 10: Creativity Detection
The AI evaluates
•	Original ideas 
•	Storytelling 
•	Examples 
•	Analogies 
•	Innovation 
Output
Creativity Score

87
________________________________________
Step 11: Emotion Analysis
Models classify writing tone.
Possible output
Confidence

High

Optimism

Medium

Empathy

High
________________________________________
Step 12: Historical Analysis
The backend loads all previous essays.
SELECT *

FROM Essays

WHERE Student_ID=101
Now calculate
Previous Average
Grammar

82

Vocabulary

80

Critical Thinking

84
Current
Grammar

91

Vocabulary

88

Critical Thinking

90
Improvement
Grammar +9

Vocabulary +8

Critical Thinking +6
________________________________________
Step 13: Recommendation Engine
A hybrid approach works well.
Rule-based logic
IF Grammar < 70

↓

Recommend grammar practice.
IF Vocabulary < 60

↓

Recommend reading editorials.
AI-generated advice
The LLM personalizes the recommendation.
Example:
Your logical reasoning has improved significantly compared to your previous essays. Focus next on adding more real-world examples to strengthen your arguments.
________________________________________
Step 14: Overall Score
A weighted scoring algorithm combines all metrics.
Example:
Overall Score =
0.20 × Grammar +
0.15 × Vocabulary +
0.30 × Critical Thinking +
0.15 × Creativity +
0.10 × Structure +
0.10 × Readability
For example:
Metric	Weight
Grammar	20%
Vocabulary	15%
Critical Thinking	30%
Creativity	15%
Structure & Organization	10%
Readability	10%
This produces a final score out of 100.
________________________________________
Step 15: Final Review Returned to the Frontend
{
  "overallScore": 89,
  "performance": "Excellent",
  "grammar": 91,
  "vocabulary": 88,
  "criticalThinking": 90,
  "creativity": 87,
  "readability": 84,
  "improvement": "+8%",
  "strengths": [
    "Strong logical arguments",
    "Good vocabulary",
    "Well-organized essay"
  ],
  "weaknesses": [
    "Add more supporting evidence",
    "Improve conclusion"
  ],
  "recommendations": [
    "Use real-life examples.",
    "Write a stronger closing paragraph."
  ]
}
What algorithms are actually used?
Stage	Algorithm / Model	Purpose
Text preprocessing	Tokenization, Lemmatization (spaCy/NLTK)	Clean and structure text
Grammar	LanguageTool	Grammar, spelling, punctuation
Readability	Flesch Reading Ease, Flesch-Kincaid, Gunning Fog	Measure reading difficulty
Semantic comparison	Sentence-BERT embeddings	Convert essays into semantic vectors
Essay similarity	Cosine Similarity	Compare with previous essays and detect repeated ideas
Historical trends	Time-series analysis (moving averages, trend lines)	Measure improvement over time
Critical thinking & creativity	LLM (e.g., GPT)	Evaluate reasoning, originality, coherence
Recommendations	Rule engine + LLM	Generate personalized, explainable feedback
Final score	Weighted scoring algorithm	Combine all metrics into one score
Why this architecture?
No single algorithm can accurately judge an essay. Grammar algorithms are good at language correctness, embeddings are good at understanding meaning, and LLMs are best at evaluating reasoning, creativity, and giving human-like feedback. Combining them produces reviews that are far more reliable and useful than relying on one AI model alone.


