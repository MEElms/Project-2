# Project-2: Data Science Programming

Using a CCM Student Survey conducted on students enrolled in Information Technology related classes, I was tasked with cleaning the data and analyzing it to evaluate how to get more students interested in IT-related courses.


## Basic Demographics

Below are the basic demographic breakdowns of the students who took the survey

#### "Number of students separated by ethnicity"
![Racial Breakdown - Bar](https://raw.githubusercontent.com/MEElms/Project-2/main/Images/Screenshot%202023-04-26%20at%202.12.50%20PM.png)

##### Code:
    df_race = df_clean.groupby('race').size().reset_index(name='count') 
    plt.barh(df_race.race,df_race['count'])  
	plt.title('Racial Breakdown of Students responding to Survey')  
	plt.show() 
  
![Racial Breakdown - Pie](https://raw.githubusercontent.com/MEElms/Project-2/main/Images/Screenshot%202023-04-26%20at%202.12.59%20PM.png)
##### Code:

    df_race = df_clean.groupby('race').size().reset_index(name='count')  
	plt.pie(df_race['count'], autopct='%1.1f%%', labels = df_race.race, pctdistance=.8)  
	plt.title("Racial Breakdown of Students responding to Survey")

#### "Number of students separated by gender"
![Gender Breakdown](https://github.com/MEElms/Project-2/blob/main/Images/Screenshot%202023-04-26%20at%202.13.06%20PM.png?raw=true)
##### Code:

    df_race = df_clean.groupby('race').size().reset_index(name='count')  
	plt.pie(df_race['count'], autopct='%1.1f%%', labels = df_race.race, pctdistance=.8)  
	plt.title("Racial Breakdown of Students responding to Survey")

#### "Number of students separated by age group"
![Age Breakdown](https://github.com/MEElms/Project-2/blob/main/Images/Screenshot%202023-04-26%20at%202.13.12%20PM.png?raw=true)
##### Code:

    df_age = df_clean.groupby('Age').size().reset_index(name='count')  
	plt.pie(df_age['count'], autopct='%1.1f%%', labels = df_age.Age, pctdistance=.8, textprops={'fontsize': 10})  
	plt.title("Age Breakdown of Students responding to Survey")
	
#### "Number of students separated by Introductory IT courses, currently enrolled in"
![Course Breakdown](https://github.com/MEElms/Project-2/blob/main/Images/Screenshot%202023-04-26%20at%202.13.21%20PM.png?raw=true)
##### Code:

    df_course = df_clean.groupby('course_enrolled').size().reset_index(name='count')  
	plt.barh(df_course.course_enrolled,df_course['count'])  
	plt.title('Course Breakdown of Students responding to Survey')  
	plt.show()
## Disaggregation of data

#### Question: What percentage of Caucasian Males under the age of 25 taking each of the introductory IT classes?
![Caucasian Males Under 25: IT-Courses](https://github.com/MEElms/Project-2/blob/main/Images/Screenshot%202023-04-26%20at%202.13.27%20PM.png?raw=true)

The pie chart shows what percentage of Caucasian, Male individuals, under age 25, that are taking IT related classes.
##### Code:

    age_mask = (df_clean['Age'] == '21-24') | (df_clean['Age'] == '19-20') | (df_clean['Age'] == '18 and younger')  
	race_mask = df_clean['race'] == 'White/Caucasian'  
	gender_mask = df_clean['Gender'] == 'Man'  
	filtered_df = df_clean[age_mask & race_mask & gender_mask]  
	white_male_25 = filtered_df.groupby('course_enrolled').size().reset_index(name='count')  
	white_male_25
	plt.pie(white_male_25['count'], autopct='%1.1f%%',labels=white_male_25.course_enrolled,pctdistance=.8, textprops={'fontsize': 10})  
	plt.title("Percentage of Students in IT related Courses that are Caucasian Males Aged < 25")

#### Question: How many/percentage of Caucasians Males, under the age of 25, are enrolled in each program at CCM that are taking introductory IT classes?
![Caucasian Males Under 25: Degree Programs](https://github.com/MEElms/Project-2/blob/main/Images/Screenshot%202023-04-26%20at%202.13.34%20PM.png?raw=true)

The pie chart shows what percentage of Degree programs Caucasian Males, under age 25, are enrolled in at CCM.
##### Code:

    wm25_program = filtered_df.groupby('degree_program').size().reset_index(name='count')  
    wm25_program
    plt.pie(wm25_program['count'], autopct='%1.1f%%',labels=wm25_program.degree_program,pctdistance=.8, textprops={'fontsize': 5})  
	plt.title("What Degree Programs are Caucasian Males Aged < 25 enrolled in at CCM")

#### Question: What do the previous two graphs look like for NON-Caucasian and NON-Male students under the age of 25 who took the survey?

###### This incredibly important questions to ask, as major of Students who took the survey were Caucasian males. What minority groups of the IT-Related Courses can be targeted to increase enrollment of IT-related programs at CCM? What groups seem to be missing altogether from the survey? (The groups that are least, or not at all, represented in the survey)

![Non-white, non-male groups: courses](https://github.com/MEElms/Project-2/blob/main/Images/Screenshot%202023-04-26%20at%202.13.41%20PM.png?raw=true)
##### Code:

    age_mask1 = (df_clean['Age'] == '21-24') | (df_clean['Age'] == '19-20') | (df_clean['Age'] == '18 and younger')  
    race_mask1 = df_clean['race'] != 'White/Caucasian'  
    gender_mask1 = (df_clean['Gender'] != 'Man')  
    filtered_df_no_wm = df_clean[age_mask1 & race_mask1 & gender_mask1]  
    nonWM_25 = filtered_df_no_wm.groupby('course_enrolled').size().reset_index(name='count')  
    nonWM_25
    plt.pie(nonWM_25['count'], autopct='%1.1f%%',labels=nonWM_25.course_enrolled,pctdistance=.8, textprops={'fontsize': 10})  
    plt.title("Percentage of Students who are NOT Caucasian Males, aged < 25 in IT related Courses")

![Non-white, non-male groups: degrees](https://github.com/MEElms/Project-2/blob/main/Images/Screenshot%202023-04-26%20at%202.13.47%20PM.png?raw=true)
##### Code:

    plt.title("Percentage of Students who are NOT Caucasian Males, aged < 25 in IT related Courses")  
    #%%  
    non_wm25_program = filtered_df_no_wm.groupby('degree_program').size().reset_index(name='count')  
    non_wm25_program
    plt.pie(non_wm25_program['count'], autopct='%1.1f%%',labels=non_wm25_program.degree_program,pctdistance=.8, textprops={'fontsize': 8})  
    plt.title("What Degree Programs are students who are Aged < 25 but NOT Caucasian Males enrolled in at CCM")

#### Insights

The information above can be utilized to target specific groups of individuals at CCM or potential students at CCM to increase enrollment in the IT related Degree Programs and IT-Related Courses.

##### Brief takeaways: 

 1. **Internet & Web-page Design** (CMP-239) is more popular among non-caucasian, non-male students under 25 at CCM.
 2. **Computer Science** (CMP-128) is more popular among caucasian, male students under 25 at CCM.
 3. The **Computer Science Degree Program** is more popular with non-caucasian, non-male students under 25 at CCM, however, the **Information Technology Degree Program** is severally under represented among the minority groups at CCM.



