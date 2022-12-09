# NFL Stochastic Analysis

Lukas Dudzik, Manav Sharma, John Curanaj, Jonathan Als

December 7, 2022

Professor John Linde

MATH 4581

![alt_text](images/image6.png "image_tooltip")

## What question are we trying to answer?

In the NFL, the top five football teams based on win percentage (as of December 4th, 2022) are the Buffalo Bills (.750 win pct.), Miami Dolphins (.727 win pct.), Philadelphia Eagles (.917 win pct.), Minnesota Vikings (.833 win pct.), and the Kansas City Chiefs (.818 win pct.). 

Although these teams currently rank the highest this season, at face value it is unclear how exactly this success is generated. For this reason, this analysis dives deeper into the offensive statistics of these five teams to answer the question: **do the offensive strategies of the top five teams in the NFL significantly differ from one another?** This information will provide a better understanding as to whether or not there is one clear offensive strategy that drives team success or if there are multiple techniques to garner success in the league. 

In order to answer the main question of the analysis, sub questions need to be answered and analyzed in order to collectively provide us the information desired. The four questions are as follow: 

* Does the number of average pass yards per game significantly differ between the five teams?
* Does the number of average rush yards per game significantly differ between the five teams?
* Do the five teams have a different average number of players with significant pass contributions?
* Do the five teams have a different average number of players with significant rush contributions?

The data from these analyses will help us answer whether or not teams have unique passing and rushing strategies, as well as if their offensive strategies are a team effort or dependent on certain star players. 

## Where did we get the data?

We needed statistics for each game of the top five football teams based on win percentage (as of December 4th, 2022).

For most of our data, we retrieved game statistics from Pro-Football-References as a csv file. This data was not very clean, so we loaded it into a Pandas dataframe in a Python notebook. 

From there, we dropped 5 columns that were undefined as NaN (not a number) values (4, 5, 6, 9, 26). We also dropped columns that we didn’t need for the analysis such as “Day”, “Date”, and “OT” (2, 3, 7). We did not need “Day” and “Date” because we already had a “Week” column to designate when the game was played. The column “OT” was removed because we did not include an overtime game as a variable in our analysis.

The data also included games that were scheduled but not played yet, so we needed to remove their values. 

Finally, as we conducted our analysis, we realized we wanted to include a more granular view of each game. We decided to include the number of players that had significant rush contributions (> 2 per game) and the number of players that had significant pass contributions (> 2 per game) for each game. 

We scraped this data manually from Google Sports, wrote it into an Excel spreadsheet, and combined it with the initial dataframe using Python.

## What stats are we using? 

For each team, four statistics were taken into account:

1. Average pass yards per game.
2. Average rush yards per game.
3. Average number of players with significant pass contributions (> 2 per game)*
4. Average number of players with significant rush contributions (> 2 per game)*

Within the data, each team’s averages were based on their first 11 games except for the Buffalo Bills, who already had 12 games worth of data.

**During an NFL game, there are many players that catch or run 1-2 times. Such a contribution was not deemed substantial enough to consider this player a significant player in the game. For this reason, only players with rush or pass contributions greater than 2 were considered in the analysis.**

ANOVA tests were run on each of the four variables separately to discover whether or not every team had the same average value. The null hypothesis (H0) in these tests was that all teams had the same mean for a variable, while the alternative hypothesis (H1) was that every team does not have statistically the same mean. Lastly, it is important to note that we were testing at the 5% level (sig = .05).

Following the completion of the ANOVA tests, tests that were rejected were followed up with a post hoc Bonferroni test. These Bonferroni tests were conducted to understand which pair of teams had significantly different mean values. The null hypothesis (H0) for each Bonferroni test was that both teams had the same mean value, while the alternative hypothesis (H1) was that both teams did not statistically have the same mean value (tested again at the 5% level).

## Results

### ANOVA Test

![alt_text](images/image1.png "image_tooltip")


After completion of the ANOVA tests we see that three of the four variables had p-values less than .05, meaning we reject the null hypothesis that all team’s mean values were the same for average pass yards (sig. = .032), average rush yards (sig. = .010), and average number of players with significant rush contributions (sig. = .004). We did however, fail to reject the null for the average number of players with significant pass contributions (sig. = .106), meaning there is no significant difference between the amount of players each top five team consistently uses for passing.  

### Post Hoc Bonferroni Tests

For the Bonferroni tests, each team was attributed with a nominal value:

1 → Bills

2 → Dolphins

3 → Eagles

4 → Vikings

5 → Chiefs

The Bonferroni test done on average pass yards has us rejecting the null between the mean values of the Eagles and Chiefs (sig. = .045). Furthermore, looking at the descriptive statistics (found in the appendix) of the data shows that the Eagles averaged 219.82 yards per game, while the Chiefs averaged 315.18 yards per game. 

The Bonferroni test done on average rush yards has us rejecting the null between the mean values of both the Eagles and Dolphins (sig. = .019) and the Eagles and Vikings (sig. = .036). Looking at the descriptive statistics, we see that the Eagles averaged 162.55 rushing yards per game while the Dolphins and Vikings averaged 94.82 and 99.36 respectively. 

The Bonferroni test done on the average number of players with significant rush contributions has us rejecting the null between the mean values of the Vikings and Bills (sig. = .037), the Vikings and Eagles (sig. = .008), and the Vikings and Chiefs (sig. = .020). Looking at the descriptive statistics, we see that the Vikings averaged 2.00 players when rushing the ball, while the Bills, Eagles and Chiefs averaged 2.92, 3.09, and 3.00 players respectively. 

## Key Insights

Based on the results shown above, some key insights were made to finalize the major takeaways discovered from the analysis: 

* Based off of the Bonferroni tests for both average pass and rush yardage, the Eagles are the only team to reject mean equivalence between at least one other team for both variables. These rejections are a result of the Eagles being the highest rushing average team and the lowest passing average team out of the five we tested. For this reason, whenever the Eagles were being tested against the opposite extreme (low rushing teams or high passing teams), the test would show that their means were not similar. Although we cannot claim that the Eagles have a completely different strategy compared to the other four teams, we can say that they are a much more running-heavy team that has found just as much success as the other four opponents.

* Although the Vikings and Bills and Vikings and Chiefs had statistically similar average rushing yards, the amount of players that contribute to those rush yardages are significantly different. This is a direct result of the Vikings high usage of All-Star running back Dalvin Cook. This is a great example of teams using different rushing strategies (focussing on one star player vs. using a collective team) to obtain the same success on the field. 

* Although the Chiefs and Eagles had statistically different average pass yardage per game, the amount of players that contribute to their passing is statistically the same. 

## Appendix

![alt_text](images/image2.png "image_tooltip")

