This contains colab notebook which has text to sql llm model evaluation
OBSERVATION :
1.	Based on the models evaluation score we can see that it is performing low on the “entities” part , medium on “logic” part and high on “syntax” part so the model produces query which are mostly syntactically correct but in “entities” part it hallucinates some knowledge sometimes	(like CGPA = 4.0 in foreign countries but in India it is 10 ) also the most ‘frequent’ entity mistake is that it always took “students” as table name instead of “student” which was given in prompt 
2.	Token count needed to be reduced in order to get only Query but still the model tried to give “explanation” or “examples” 
3.	Latency reduced when decreased both input and output token count

LOGS :

[
    {
        "prompt": "You are a SQL generator which returns only one valid SQL query for the sentence.\n Schema : tables :['student'], columns: [student_id(INT),student_name(CHAR),CGPA(FLOAT),Internships(INT)].\nSentence: List students with CGPA > 8.0.\n SQL_query: ",
        "SQL-query": "SELECT student_id, student_name, CGPA, Internships FROM students WHERE CGPA > 8.0;",
        "evaluation": {
            "entity_score": 0,
            "syntax_score": 1,
            "logic_score": 1
        },
        "latency": 28.945062160491943,
        "tokens": 106
    },
    {
        "prompt": "You are a SQL generator which returns only one valid SQL query for the sentence.\n Schema : tables :['student'], columns: [student_id(INT),student_name(CHAR),CGPA(FLOAT),Internships(INT)].\nSentence: List students with Internships > 2.\n SQL_query: ",
        "SQL-query": "SELECT student_id, student_name, CGPA, Internships FROM students WHERE Internships > 2;",
        "evaluation": {
            "entity_score": 0,
            "syntax_score": 1,
            "logic_score": 1
        },
        "latency": 28.711746215820312,
        "tokens": 104
    },
    {
        "prompt": "You are a SQL generator which returns only one valid SQL query for the sentence.\n Schema : tables :['student'], columns: [student_id(INT),student_name(CHAR),CGPA(FLOAT),Internships(INT)].\nSentence: Show all students with CGPA < 6.5.\n SQL_query: ",
        "SQL-query": "SELECT * FROM student WHERE CGPA < 6.5;",
        "evaluation": {
            "entity_score": 1,
            "syntax_score": 1,
            "logic_score": 1
        },
        "latency": 29.638261556625366,
        "tokens": 107
    },
    {
        "prompt": "You are a SQL generator which returns only one valid SQL query for the sentence.\n Schema : tables :['student'], columns: [student_id(INT),student_name(CHAR),CGPA(FLOAT),Internships(INT)].\nSentence: Find students with exactly 3 Internships.\n SQL_query: ",
        "SQL-query": "SELECT student_id, student_name, CGPA, COUNT(INTERNSHIP_ID) FROM student INNER JOIN internships ON student.",
        "evaluation": {
            "entity_score": 1,
            "syntax_score": 1,
            "logic_score": 0
        },
        "latency": 28.320101499557495,
        "tokens": 104
    },
    {
        "prompt": "You are a SQL generator which returns only one valid SQL query for the sentence.\n Schema : tables :[student], columns: [student_id(INT),student_name(CHAR),CGPA(FLOAT),Internships(INT)].\nSentence: Display students whose CGPA is between 7.0 and 9.0.\n SQL_query: ",
        "SQL-query": "SELECT * FROM students WHERE CGPA BETWEEN 7.0 AND 9.0;",
        "evaluation": {
            "entity_score": 0,
            "syntax_score": 1,
            "logic_score": 1
        },
        "latency": 30.93771243095398,
        "tokens": 112
    },
    {
        "prompt": "You are a SQL generator which returns only one valid SQL query for the sentence.\n Schema : tables :[student], columns: [student_id(INT),student_name(CHAR),CGPA(FLOAT),Internships(INT)].\nSentence: Count the total number of students.\n SQL_query: ",
        "SQL-query": "SELECT COUNT(*) FROM student;",
        "evaluation": {
            "entity_score": 1,
            "syntax_score": 1,
            "logic_score": 1
        },
        "latency": 27.851612091064453,
        "tokens": 102
    },
    {
        "prompt": "You are a SQL generator which returns only one valid SQL query for the sentence.\n Schema : tables :[student], columns: [student_id(INT),student_name(CHAR),CGPA(FLOAT),Internships(INT)].\nSentence: Get the average CGPA of students.\n SQL_query: ",
        "SQL-query": "SELECT AVG(CGPA) FROM student WHERE Internships = 1;",
        "evaluation": {
            "entity_score": 0,
            "syntax_score": 1,
            "logic_score": 0
        },
        "latency": 28.15555477142334,
        "tokens": 103
    },
    {
        "prompt": "You are a SQL generator which returns only one valid SQL query for the sentence.\n Schema : tables :[student], columns: [student_id(INT),student_name(CHAR),CGPA(FLOAT),Internships(INT)].\nSentence: Find students with no Internships.\n SQL_query: ",
        "SQL-query": "SELECT * FROM students WHERE Internships = 0;",
        "evaluation": {
            "entity_score": 0,
            "syntax_score": 1,
            "logic_score": 1
        },
        "latency": 27.885423183441162,
        "tokens": 102
    },
    {
        "prompt": "You are a SQL generator which returns only one valid SQL query for the sentence.\n Schema : tables :[student], columns: [student_id(INT),student_name(CHAR),CGPA(FLOAT),Internships(INT)].\nSentence: List students ordered by CGPA descending.\n SQL_query: ",
        "SQL-query": "SELECT student_id, student_name, CGPA, Internships FROM students WHERE CGPA > 3.00 ORDER BY CGPA DESC",
        "evaluation": {
            "entity_score": 0,
            "syntax_score": 1,
            "logic_score": 0
        },
        "latency": 28.8799729347229,
        "tokens": 104
    },
    {
        "prompt": "You are a SQL generator which returns only one valid SQL query for the sentence.\n Schema : tables :[student], columns: [student_id(INT),student_name(CHAR),CGPA(FLOAT),Internships(INT)].\nSentence: Show top 5 students by CGPA.\n SQL_query: ",
        "SQL-query": "SELECT * FROM students WHERE CGPA >= 3.00 ORDER BY CGPA DESC LIMIT 5;",
        "evaluation": {
            "entity_score": 0,
            "syntax_score": 1,
            "logic_score": 0
        },
        "latency": 29.38087034225464,
        "tokens": 104
    },
    {
        "prompt": "You are a SQL generator which returns only one valid SQL query for the sentence.\n Schema : tables :[student], columns: [student_id(INT),student_name(CHAR),CGPA(FLOAT),Internships(INT)].\nSentence: List students with CGPA >= 9.0 and Internships >= 1.\n SQL_query: ",
        "SQL-query": "SELECT * FROM students WHERE CGPA >= 9.0 AND Internships >= 1;",
        "evaluation": {
            "entity_score": 0,
            "syntax_score": 1,
            "logic_score": 1
        },
        "latency": 32.102885007858276,
        "tokens": 112
    },
    {
        "prompt": "You are a SQL generator which returns only one valid SQL query for the sentence.\n Schema : tables :[student], columns: [student_id(INT),student_name(CHAR),CGPA(FLOAT),Internships(INT)].\nSentence: Find students whose student_name starts with 'A'.\n SQL_query: ",
        "SQL-query": "SELECT * FROM students WHERE student_name LIKE 'A%';",
        "evaluation": {
            "entity_score": 0,
            "syntax_score": 1,
            "logic_score": 1
        },
        "latency": 29.63054871559143,
        "tokens": 106
    },
    {
        "prompt": "You are a SQL generator which returns only one valid SQL query for the sentence.\n Schema : tables :[student], columns: [student_id(INT),student_name(CHAR),CGPA(FLOAT),Internships(INT)].\nSentence: Find students whose student_name contains 'Kumar'.\n SQL_query: ",
        "SQL-query": "SELECT * FROM students WHERE student_name LIKE 'Kumar';",
        "evaluation": {
            "entity_score": 0,
            "syntax_score": 1,
            "logic_score": 1
        },
        "latency": 29.19271159172058,
        "tokens": 106
    },
    {
        "prompt": "You are a SQL generator which returns only one valid SQL query for the sentence.\n Schema : tables :[student], columns: [student_id(INT),student_name(CHAR),CGPA(FLOAT),Internships(INT)].\nSentence: Get the maximum CGPA.\n SQL_query: ",
        "SQL-query": "SELECT MAX(CGPA) FROM student WHERE Internships = 1;",
        "evaluation": {
            "entity_score": 1,
            "syntax_score": 1,
            "logic_score": 0
        },
        "latency": 29.010979652404785,
        "tokens": 101
    },
    {
        "prompt": "You are a SQL generator which returns only one valid SQL query for the sentence.\n Schema : tables :[student], columns: [student_id(INT),student_name(CHAR),CGPA(FLOAT),Internships(INT)].\nSentence: Get the minimum CGPA.\n SQL_query: ",
        "SQL-query": "SELECT min(CGPA) FROM student WHERE Internships = 1;",
        "evaluation": {
            "entity_score": 1,
            "syntax_score": 1,
            "logic_score": 0
        },
        "latency": 28.254294872283936,
        "tokens": 101
    },
    {
        "prompt": "You are a SQL generator which returns only one valid SQL query for the sentence.\n Schema : tables :[student], columns: [student_id(INT),student_name(CHAR),CGPA(FLOAT),Internships(INT)].\nSentence: Count students with CGPA above 8.5.\n SQL_query: ",
        "SQL-query": "SELECT student_id, student_name, CGPA, Internships FROM students WHERE CGPA > 8.5;",
        "evaluation": {
            "entity_score": 0,
            "syntax_score": 1,
            "logic_score": 1
        },
        "latency": 29.16294813156128,
        "tokens": 106
    },
    {
        "prompt": "You are a SQL generator which returns only one valid SQL query for the sentence.\n Schema : tables :[student], columns: [student_id(INT),student_name(CHAR),CGPA(FLOAT),Internships(INT)].\nSentence: List students with Internships less than 1.\n SQL_query: ",
        "SQL-query": "SELECT student_id, student_name, CGPA, Internships FROM students WHERE Internships < 1;",
        "evaluation": {
            "entity_score": 0,
            "syntax_score": 1,
            "logic_score": 1
        },
        "latency": 29.811538457870483,
        "tokens": 105
    },
    {
        "prompt": "You are a SQL generator which returns only one valid SQL query for the sentence.\n Schema : tables :[student], columns: [student_id(INT),student_name(CHAR),CGPA(FLOAT),Internships(INT)].\nSentence: Show students sorted by Internships ascending.\n SQL_query: ",
        "SQL-query": "SELECT student_id, student_name, CGPA, Internships FROM students WHERE Internships > 0 ORDER BY Internships ASC;",
        "evaluation": {
            "entity_score": 0,
            "syntax_score": 1,
            "logic_score": 0
        },
        "latency": 28.636674404144287,
        "tokens": 104
    },
    {
        "prompt": "You are a SQL generator which returns only one valid SQL query for the sentence.\n Schema : tables :[student], columns: [student_id(INT),student_name(CHAR),CGPA(FLOAT),Internships(INT)].\nSentence: Find students with CGPA not equal to 7.0.\n SQL_query: ",
        "SQL-query": "SELECT * FROM students WHERE CGPA <> 7.0;",
        "evaluation": {
            "entity_score": 0,
            "syntax_score": 1,
            "logic_score": 1
        },
        "latency": 29.826392889022827,
        "tokens": 108
    },
    {
        "prompt": "You are a SQL generator which returns only one valid SQL query for the sentence.\n Schema : tables :[student], columns: [student_id(INT),student_name(CHAR),CGPA(FLOAT),Internships(INT)].\nSentence: List student_name and CGPA only.\n SQL_query: ",
        "SQL-query": "SELECT student_name, CGPA FROM students WHERE CGPA > 3.00;",
        "evaluation": {
            "entity_score": 0,
            "syntax_score": 1,
            "logic_score": 0
        },
        "latency": 28.306333303451538,
        "tokens": 104
    },
    {
        "average tokens": 105.05
    },
    {
        "average latency": 29.13208121061325
    },
    {
        "Total_eval_score": "evaluation : entity 5, syntax 20, logic 12"
    }
]
