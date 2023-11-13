# Pandas-Challenge

# District Summary
Include the following in a DataFrame:
  - Total number of unique schools
      - I was able to collect this information by using the nunique() method

          school_count = school_data_complete["school_name"].nunique()
          school_count

      - **Code for the nunique() method was taken from https://practicaldatascience.co.uk/data-science/how-to-identify-and-count-unique-values-in-pandas#:~:text=To%20count%20the%20number%20of,the%20number%20of%20unique%20values**
  - Total students
      - I again used the nunique() method to get this number. I calculated the nunique() of the Student ID column

          student_count = school_data_complete["Student ID"].nunique()
          student_count

      - **Code for the nunique() method was taken from https://practicaldatascience.co.uk/data-science/how-to-identify-and-count-unique-values-in-pandas#:~:text=To%20count%20the%20number%20of,the%20number%20of%20unique%20values**
  - Total budget
      - I took the unique budgets from the budget column (because each district has a budget) and thhen took the sum of those budgets.
   
          unique_budgets = school_data_complete["budget"].unique()
          total_budget = unique_budgets.sum()
          total_budget

      - **Code for this section was taken from class activities**
  - Average math score
      - I used the mean function to pull the average math score

          average_math_score = school_data_complete["math_score"].mean()
          average_math_score

      - **Code for this section was taken from class activities**
  - Average reading score
      - I used the mean function to pull the average reading score

          average_reading_score = school_data_complete["reading_score"].mean()
          average_reading_score

      - **Code for this section was taken from class activities**
  - % passing math (the percentage of students who passed math)
      - This code was provided in the starter code. Basically counted the student names that had a math score greater or equal to 70

          passing_math_count = school_data_complete[(school_data_complete["math_score"] >= 70)].count()["student_name"]
          passing_math_percentage = passing_math_count / float(student_count) * 100
          passing_math_percentage
        
  - % passing reading (the percentage of students who passed reading)
      - This code was provided in the starter code. Basically counted the student names that had a reading score greater or equal to 70

          passing_reading_count = school_data_complete[(school_data_complete["reading_score"] >= 70)].count()["student_name"]
          passing_reading_percentage = passing_reading_count / float(student_count) * 100
          passing_reading_percentage

  - % overall passing (the percentage of students who passed math AND reading)
      - This code was provided in the starter code. Basically counted students with math AND reading score greater or equal to 70

          passing_math_reading_count = school_data_complete[
              (school_data_complete["math_score"] >= 70) & (school_data_complete["reading_score"] >= 70)
              ].count()["student_name"]
          overall_passing_rate = passing_math_reading_count /  float(student_count) * 100
          overall_passing_rate

  - Last part of this section was to put everything together in a dataframe
      - Used pd.DataFrame to create the dataframe. Just had to create a dictionary with the column names as the keys and then the variables from the earlier activities as values
      - The formatting part of this code was prodived in the starter code

          district_summary = pd.DataFrame({"Total Schools": school_count, "Total Students": student_count, "Total Budget":                           total_budget, "Average Math Score": average_math_score, "Average Reading Score": average_reading_score, 
                "% Passing Math": passing_math_percentage, "% Passing Reading": passing_reading_percentage,
                "5 Overall Passing": overall_passing_rate})

          # Formatting
          district_summary["Total Students"] = district_summary["Total Students"].map("{:,}".format)
          district_summary["Total Budget"] = district_summary["Total Budget"].map("${:,.2f}".format)

          # Display the DataFrame
          district_summary

      - **Code for this was taken from activities we performed in class about how to create DataFrames**


# School Summary
Include the following in a DataFrame: 
  - School name
      - The school names were included by grouping the data for the rest of the results by school name

  - School type
      - I first grouped by the school name and use max() to pull the max value of the type column. This returned the type for each school

          school_group_by = school_data_complete.groupby(["school_name"])
          school_types = school_group_by["type"].max()

          school_types

      - **Code for this was taken from the groupby activies we did in class. As well as activies where we covered max, count, etc.**

  - Total students
      - I referenced my grouped by variable I had created above and then used the count() function of the student ID column

          per_school_counts = school_group_by["Student ID"].count()
          per_school_counts

    - **Code for this was taken from the groupby activies we did in class. As well as activies where we covered max, count, etc.**

  - Total school budget
      - I referenced my grouped by variable I had created above and then used unique() to pull the budgets for each school
      - I then formatted the column as a float because I was having issues later on when trying to format my DataFrame

          per_school_budget = per_school_budget.astype(float)
          per_school_budget = per_school_budget.astype(float)
          per_school_budget

    - **Code for the unique() part of this was taken from activities in class. I got the idea to format this to float from ChatGPT when I was having issues later on. I decided to put in this cell to format it right away**

  - Per student budget
      - I divided the budget I had calculated from the previous problem by the per school counts variable I had from earlier
      - I also formatted this column to float to fix the issues I was having later on with my DataFrame
   
          per_school_capita = per_school_budget / per_school_counts
          per_school_capita = per_school_capita.astype(float)
          per_school_capita

      - **Code for this was taken from similar activites we did in class. Idea for formatting this to float was taken from ChatGPT**

  - Average math score
      - I calculated this by using grouped by variable from earlier and then taking the mean() of it

          per_school_math = school_group_by["math_score"].mean()
          per_school_math

      - **Code for this was taken from activities in class**

  - Average reading score
      - I calculated this by using grouped by variable from earlier and then taking the mean() of it
   
          per_school_reading = school_group_by["reading_score"].mean()
          per_school_reading

      - **Code for this was taken from activities in class**

  - % passing math (the percentage of students who passed math)
      - To calculate this I used loc to filter the results to only rows with math scores greater or equal to 70
      - I then referenced that variable, grouped by school name, and then took the count of the student ID column
   
          students_passing_math = school_data_complete.loc[school_data_complete["math_score"] >= 70, :]
          school_students_passing_math = students_passing_math.groupby("school_name")["Student ID"].count()
          school_students_passing_math

      - **Most of the code for this was taken from activities in class, but I was getting errors. ChatGPT helped me clena up my code and make sure I was using () and [] properly**

  - % passing reading (the percentage of students who passed reading)
      - To calculate this I used loc to filter the results to only rows with reading scores greater or equal to 70
      - I then referenced that variable, grouped by school name, and then took the count of the student ID column

          students_passing_reading = school_data_complete.loc[school_data_complete["reading_score"] >= 70, :]
          school_students_passing_reading = students_passing_reading.groupby("school_name")["Student ID"].count()
          school_students_passing_reading

      - **Most of the code for this was taken from activities in class, but I was getting errors. ChatGPT helped me clena up my code and make sure I was using () and [] properly**

  - % overall passing (the percentage of students who passed math AND reading)
      - This was provided in the starter code.
   
          students_passing_math_and_reading = school_data_complete[
                  (school_data_complete["reading_score"] >= 70) & (school_data_complete["math_score"] >= 70)]
          school_students_passing_math_and_reading = students_passing_math_and_reading.groupby(["school_name"]).size()
          school_students_passing_math_and_reading

      - **Code was provided in the starter code for this problem**

  - Highest-Performing Schools (by % Overall Passing)
      - This was also provided in the starter code. Didn't have to do anything here.

          per_school_passing_math = school_students_passing_math / per_school_counts * 100
          per_school_passing_reading = school_students_passing_reading / per_school_counts * 100
          overall_passing_rate = school_students_passing_math_and_reading / per_school_counts * 100

  - Last part of this section was to put everything together in a DataFrame
      - Similar to the first part of the assignment I used the pd.DataFrame method to create my DataFrame. I used a dictionary with the key as the column name and the value as the variables I had created throughout the assignment.
   
          per_school_summary = pd.DataFrame({"School Type": school_types, "Total Students": per_school_counts,
                                   "Total School Budget": per_school_budget, "Per Student Budget": per_school_capita,
                                  "Average Math Score": per_school_math, "Average Reading Score": per_school_reading,
                                   "% Passing Math": per_school_passing_math, "% Passing Reading": per_school_passing_reading,
                                  "% Overall Passing": overall_passing_rate})

          # Formatting
          per_school_summary["Total School Budget"] = per_school_summary["Total School Budget"].map("${:,.2f}".format)
          per_school_summary["Per Student Budget"] = per_school_summary["Per Student Budget"].map("${:,.2f}".format)

          #Drop the name of the index for my final output
          per_school_summary.index.name = None
          # Display the DataFrame
          per_school_summary

      - **Code for this was taken from activites in class. I did search chatGPT for a way to drop the name of the index but that was also provided later on in the code**
   
# Highest-Performing Schools (by % Overall Passing)
  - Sort the schools by % Overall Passing in descending order and display the top 5 rows. Save the results in a DataFrame called "top_schools".
      - I used the sort method we used in class in order to sort the results in the desired format. Set ascending = to False to sort top to bottom.

          top_schools = per_school_summary.sort_values("% Overall Passing", ascending=False)
          top_schools.head(5)

      - **Code for this was taken the sort activity we performed in class**

# Lowest-Performing Schools (by % Overall Passing)
  - Sort the schools by % Overall Passing in ascending order and display the top 5 rows. Save the results in a DataFrame called "bottom_schools".
      - Again used the sort method we used in class in order to sort the results in the desired format. Set ascneding = to True to sort bottom to top.
   
          bottom_schools = per_school_summary.sort_values("% Overall Passing", ascending=True)
          bottom_schools.head(5)

      - **Code for this was taken the sort activity we performed in class**

# Math Scores by Grade
- Perform the necessary calculations to create a DataFrame that lists the average math score for students of each grade level (9th, 10th, 11th, 12th) at each school.
    - First we used the code provided to separate the data by grade
    - Then we grouped by the school name and took the math score mean for the each respective grade
    - Finally we created a new DataFrame and plugged in the desired data.
 
        ninth_graders = school_data_complete[(school_data_complete["grade"] == "9th")]
        tenth_graders = school_data_complete[(school_data_complete["grade"] == "10th")]
        eleventh_graders = school_data_complete[(school_data_complete["grade"] == "11th")]
        twelfth_graders = school_data_complete[(school_data_complete["grade"] == "12th")]

        # Group by `school_name` and take the mean of the `math_score` column for each.
        ninth_grade_math_scores = ninth_graders.groupby("school_name")["math_score"].mean()
        tenth_grader_math_scores = tenth_graders.groupby("school_name")["math_score"].mean()
        eleventh_grader_math_scores = eleventh_graders.groupby("school_name")["math_score"].mean()
        twelfth_grader_math_scores = twelfth_graders.groupby("school_name")["math_score"].mean()

        # Combine each of the scores above into single DataFrame called `math_scores_by_grade`
        math_scores_by_grade = pd.DataFrame({"9th": ninth_grade_math_scores, "10th": tenth_grader_math_scores,
                                    "11th": eleventh_grader_math_scores, "12th": twelfth_grader_math_scores})

        # Minor data wrangling
        math_scores_by_grade.index.name = None

        # Display the DataFrame
        math_scores_by_grade

    - **Code for this was mostly taken from activities in class and copied from how it was used earlier. A lot of this code was in the starter code we just had to plug in the desired information**

# Reading Scores by Grade
  - Create a DataFrame that lists the average reading score for students of each grade level (9th, 10th, 11th, 12th) at each school.
      - First we used the code provided to separate the data by grade
      - Then we grouped by the school name and took the reading score mean for the each respective grade
      - Finally we created a new DataFrame and plugged in the desired data.
   
          ninth_graders = school_data_complete[(school_data_complete["grade"] == "9th")]
          tenth_graders = school_data_complete[(school_data_complete["grade"] == "10th")]
          eleventh_graders = school_data_complete[(school_data_complete["grade"] == "11th")]
          twelfth_graders = school_data_complete[(school_data_complete["grade"] == "12th")]

          # Group by `school_name` and take the mean of the the `reading_score` column for each.
          ninth_grade_reading_scores = ninth_graders.groupby("school_name")["reading_score"].mean()
          tenth_grader_reading_scores = tenth_graders.groupby("school_name")["reading_score"].mean()
          eleventh_grader_reading_scores = eleventh_graders.groupby("school_name")["reading_score"].mean()
          twelfth_grader_reading_scores = twelfth_graders.groupby("school_name")["reading_score"].mean()

          # Combine each of the scores above into single DataFrame called `reading_scores_by_grade`
          reading_scores_by_grade = pd.DataFrame({"9th": ninth_grade_reading_scores, "10th": tenth_grader_reading_scores,
                                    "11th": eleventh_grader_reading_scores, "12th": twelfth_grader_reading_scores})

          # Minor data wrangling
          reading_scores_by_grade = reading_scores_by_grade[["9th", "10th", "11th", "12th"]]
          reading_scores_by_grade.index.name = None

          # Display the DataFrame
          reading_scores_by_grade

      - **Code for this was mostly taken from activities in class and copied from how it was used earlier. A lot of this code was in the starter code we just had to plug in the desired information**


# Scores by School Spending
  - Use pd.cut with the provided code to bin the data by the spending ranges (2 points)
      - I was having some trouble with this one so I first removed the $ and , from the per student budget column.
      - Then I used pd.cut to bin the data into the spending ranges
      - Then I reformatted the per student budget column to include the $ that I removed.
   
          school_spending_df["Per Student Budget"] = pd.to_numeric(school_spending_df["Per Student Budget"].replace('[\$,]', '',                     regex=True), errors='coerce')
          school_spending_df["Spending Ranges (Per Student)"] = pd.cut(school_spending_df["Per Student Budget"], spending_bins,                      labels=labels)
          school_spending_df["Per Student Budget"] = school_spending_df["Per Student Budget"].map("${:,.2f}".format)
          school_spending_df

      - **The code for the bins was taken from the activities we had in class. The code to remove the symbols was taken from chatGPT. Code to reformat the column was taken from activites we did in class**
        
  - Use the code provided to calculate the averages (1 points)
      - For this I grouped by the spending ranges and then used mean() for the columns
   
          spending_math_scores = school_spending_df.groupby(["Spending Ranges (Per Student)"])["Average Math Score"].mean()
          spending_reading_scores = school_spending_df.groupby(["Spending Ranges (Per Student)"])["Average Reading Score"].mean()
          spending_passing_math = school_spending_df.groupby(["Spending Ranges (Per Student)"])["% Passing Math"].mean()
          spending_passing_reading = school_spending_df.groupby(["Spending Ranges (Per Student)"])["% Passing Reading"].mean()
          overall_passing_spending = school_spending_df.groupby(["Spending Ranges (Per Student)"])["% Overall Passing"].mean()

      - **This code was provided with the starter code**
  - Create the spending_summary DataFrame using the binned and averaged spending data (2 points)
      - Just used pd.DataFrame to put the data into a DataFrame
   
          spending_summary = pd.DataFrame({"Average Math Score": spending_math_scores, "Average Reading Score":                                       spending_reading_scores, "% Passing Math": spending_passing_math, "% Passing Reading": spending_passing_reading,
                  "%Overall Passing": overall_passing_spending})

          # Display results
          spending_summary

      - **Code for this was taken from activites performed in class**

# Scores by School Size (5 points)
  - Use pd.cut with the provided code to bin the data by the school sizes (2 points)
    - Used pd.cut to put the bin the data in the DataFrame

          per_school_summary["School Size"] = pd.cut(school_spending_df["Total Students"], size_bins, labels=labels)
          per_school_summary

    - **Code for this was provided from activities in class**
   
  - Use the code provided to calculate the averages (1 points)
      - For this I grouped by the spending ranges and then used mean() for the column
   
          size_math_scores = per_school_summary.groupby(["School Size"])["Average Math Score"].mean()
          size_reading_scores = per_school_summary.groupby(["School Size"])["Average Reading Score"].mean()
          size_passing_math = per_school_summary.groupby(["School Size"])["% Passing Math"].mean()
          size_passing_reading = per_school_summary.groupby(["School Size"])["% Passing Reading"].mean()
          size_overall_passing = per_school_summary.groupby(["School Size"])["% Overall Passing"].mean()

      - **Code for this was in the starter code**
   
  - Create the size_summary DataFrame using the binned and averaged size data (2 points)
      - Just used pd.DataFrame to create a DataFrame
   
          size_summary = pd.DataFrame({"Average Math Score": size_math_scores, "Average Reading Score": size_reading_scores,
                            "% Passing Math": size_passing_math, "% Passing Reading": size_passing_reading, 
                            "% Overall Passing": size_overall_passing})

          # Display results
          size_summary

      - **Code for this was provided in class**

# Scores by School Type (5 points)
  - Group the per_school_summary DataFrame by "School Type" and average the results (2 points)
      - This was provided in the starter code

          average_math_score_by_type = per_school_summary.groupby(["School Type"])["Average Math Score"].mean()
          average_reading_score_by_type = per_school_summary.groupby(["School Type"])["Average Reading Score"].mean()
          average_percent_passing_math_by_type = per_school_summary.groupby(["School Type"])["% Passing Math"].mean()
          average_percent_passing_reading_by_type = per_school_summary.groupby(["School Type"])["% Passing Reading"].mean()
          average_percent_overall_passing_by_type = per_school_summary.groupby(["School Type"])["% Overall Passing"].mean()

      - **Code for this was provided in the starter code**
   
  - Create a new DataFrame called type_summary that uses the new column data (2 points)
      - Used pd>dataFrame to create a DataFrame
   
          type_summary = pd.DataFrame({"Average Math Score": average_math_score_by_type, "Average Reading Score":                                       average_reading_score_by_type, "% Passing Math": average_percent_passing_math_by_type, "% Passing Reading":                         average_percent_passing_reading_by_type, "% Overall Passing": average_percent_overall_passing_by_type})

          # Display results
          type_summary

      - **Code for this was provided in the starter code**
   
# Written Report
  - Summarize the results.

    This analysis is performed for this city's school district. We are looking at all schools in the area and looking for trends to help make strategic decisions regarding future school budgets and priorities. We start this analysis by looking at a summary of all the data we have available for this district. By looking at the data at this level we are able to see some of our district's overall stats such as average math score (78.985371), average reading score (81.87784), and overall passing percentage (65.172326). We also are able to see that our total budget for the district is $24,649,428.00 and we have a total of 39,170 students across 15 schools.
    
    As we continue our analysis we breakdown these numbers per school and dive into each school's numbers to thoroughly analyze where each school is at. This information is helpful to see information such as which schools are performing the best/worse, which schools has the most/least students, and the budget of each individual school. This information may be helpful to helping us make decisions about which schools might needs more resources. Looking at this data we see that the top three schools in the Overall Passing Percentage are Cabrera High School, Thomas High School, and Griffin High school. The three schools that are performing the worst in the Overall Passing Percentage are Rodriguez High School, Figueroa High School, and Huang High School. Interestingly enough the per student budget for the schools performing the worst are overall higher than the three best performing schools.
     
    The next part of our analysis is to dig deeper into the data and look at the scores for both reading and math by grade. This gives us insight into what grades are doing well or poorly in these areas and how they are progressing through their tenure at the school. Most of these schools have students performing relatively the same throughout their high school tenure with only a few that are significantly different over the 4 years.
    
    Next we take a look at the test scores by school spending. In this part of the analysis we are able to see if there is a positive relationship between budgets and school spending. This data shows us some interesting results. It seems that as school spending per student decreases we are seeing better test scores. There can be other factors at play here, but this is an interesting discovery as you would typically expect the opposite.

    The final part of the analysis is to take a look at test scores by school size and school type. This should indicate whether there is a relationship between the number of students per school and their test scores. It should also give us some information as to what impact school type may have on test scores. As you might expect as the number of students per school increases we are seeing a decrease in scores. It's not as noticeable going from small to medium school size, but is very noticeable as you go from medium to large. Another intersting part of this analysis is that Charter schools have much higher scores and overall passing percentages than District schools.

  - Draws two correct conclusions or comparisons from the calculations

      1. One of the most significant conclusions we can draw from this analysis is that the number of students within a school has a large impact on the test scores of that school. We can see that by looking at a few different parts of our analysis. The section showing the Highest Performing Schools and Lowest Performance Schools are the first areas that demonstrate this. You can see that the number of students in the top performing schools is at least several hundred below the lowest performance schools. The lowest performance schools have on average the highest number of students. This is supported in a roundabout way by looking at the scores by school spending analysis. There doesn't seem to be a positive impact in having a higher per student budget. In fact it decreases steadily as you have a higher budget per student. This gives more weight to idea that more students at a school results in lower test scores. Finally, we can see this in the scores by school size analysis. The large school size bracket has significantly lower test scores and overall passing percentages than the small and medium school size brackets. This points towards the conclusion that school size can have a drastic impact on test scores.
      2. Another conclusion that we can draw from this data is that charter schools result in better test results than district schools. We can see this by looking at the Scores by School Type analysis. The average math and reading scores are relatively close between these two categories, but the percentage passing both and the overall passing percentage are extremely higher at charter schools. We can also see by looking at the per student budget that charter schools tend to have lower budgets than district schools. Despite having lower budgets they tend to have higher passing rates. Charter schools also have a smaller number of students per school than district schools. This could play a factor in the higher scores at charter schools. Charter schools also offer more flexible class options and a more diverse curriculum. This could contribute to students being more engaged in class. Regardless of the reasons it seems charter schools have significantly higher passing rates than district schools. 
