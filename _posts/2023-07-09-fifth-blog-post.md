Project 2 Reflection
================
Simon Weisenhorn
2023-07-09

This blog is to reflect on my efforts to in completing the second
project in ST 558. I found this project to be less demanding than the
first one, but was certainly still challenging overall. For my portion
of the work, I wrote the entire introduction to inform the readers of
the necessary background information and to prepare them for what to
expect throughout the report. I also wrote a very helpful function that
aimed to take in a character string of a given data channel and then
subset the data based on the character string, as well as remove the
opposing data channels and non-predictive variables from the resulting
dataframe. This function was helpful because it assisted in the
automation process of the entire project because I was able to feed it a
new channel string for each iteration of the loop that rendered all of
the reports. Following the creation of this function, I worked hard to
create interesting and meaningful summaries through utilizing colors and
different graphs, which were accompanied by generic descriptions of what
the reader could expect to understand from the graph based on what the
data looked like for a particular channel. Finally, for my final portion
of the project, I built a linear model that included interactions
between all of the variables, and a boosted tree model. Both of these
models used preprocessed data and cross-validation to ensure a higher
accuracy for predicting the test set, and the boosted tree model was
accompanied by a brief explanation into the model itself.

Overall, I learned a lot from this project on how helpful automating an
.Rmd file can be, while continuing to challenge my problem solving and
creative skills through creating helpful functions and exploring
interesting visualizations. My biggest takeaway was that I should always
look to see where I can add to my code so that automation can become
relevant and effective for any future analyzes. Additionally, I think
the most difficult part of the for me was figuring out the automation
process because the random forest models took so long to render and I
kept running into errors with the parameters. I also struggled with
coordinating push/pull requests with my partner because I have not
worked with a collaborator in Github before. The biggest thing that I
would do differently in approaching a similar project would be to wait
to render the random forest model until the very end. In doing this, I
could make sure that the code would correctly render each document by
the specific parameter and not have to wait on the random forest model
to run every time. This would’ve helped me reduce the amount of time it
took to trouble shoot why every outputted report was returning
information about the lifestyle channel instead of all of the different
channels.

Please enjoy exploring the reports below!

Here is the link to my github pages repo:
[LINK](https://saziz12.github.io/ST558-Project2/)  
Here is the link to my regular repo:
[LINK](https://github.com/saziz12/ST558-Project2)
