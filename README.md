\documentclass[10pt,twocolumn,letterpaper]{article}
%% Welcome to Overleaf!
%% If this is your first time using LaTeX, it might be worth going through this brief presentation:
%% https://www.overleaf.com/latex/learn/free-online-introduction-to-latex-part-1

%% Researchers have been using LaTeX for decades to typeset their papers, producing beautiful, crisp documents in the process. By learning LaTeX, you are effectively following in their footsteps, and learning a highly valuable skill!

%% The \usepackage commands below can be thought of as analogous to importing libraries into Python, for instance. We've pre-formatted this for you, so you can skip right ahead to the title below.

%% Language and font encodings
\usepackage[english]{babel}
\usepackage[utf8x]{inputenc}
\usepackage[T1]{fontenc}

%% Sets page size and margins
\usepackage[a4paper,top=3cm,bottom=2cm,left=3cm,right=3cm,marginparwidth=1.75cm]{geometry}

%% Useful packages
\usepackage{amsmath}
\usepackage{graphicx}
\usepackage[colorinlistoftodos]{todonotes}
\usepackage[colorlinks=true, allcolors=blue]{hyperref}
\usepackage{natbib}
\bibliographystyle{unsrt}
%% Title
\title{
		\usefont{OT1}{bch}{b}{n}
		\normalfont \normalsize \textsc{CS152 - Sports Analytics} \\ [10pt]
		\huge Assigning Values to NBA Draft Picks via Estimated Wins Added (EWA) \\
}
\selectlanguage{english}
\usepackage{authblk}
\author{Connor Townson}
\affil{Tufts University}

\begin{document}
\maketitle

\section{Introduction}

In the modern NBA, draft picks have an immense amount of value. For rebuilding teams, they serve as the primary mechanism for acquiring young talent to build around. For contending teams, they're seen as trade assets that can be used to acquire superstar-level talent from lesser-contending teams. Yet, despite their major role in roster construction, the value they bring is fairly uncertain and varies from year to year.

The success of an NBA prospect depends on a variety of factors, such as the team they were drafted to and how they adjust to professional play. This raises concern for many rebuilding teams, as they can't afford to spend too many years waiting for their young talent to reach their potential. According to recent trends exhibited by the 2025 Oklahoma City Thunder and Cleveland Cavaliers, the common timeline for a rebuilding NBA team to reach its contending window is 3-5 seasons \cite{Rebuild}. The first two seasons consist of the team selling off its existing talent for future picks. This noticeably weaker roster influences the team to lose a large number of games to increase their chances of a higher draft pick in a process known as "tanking".

As the third season approaches, the rebuilding team is now looking to acquire its young talent through the draft. It will then develop these players over the next three seasons, working to increase their win total to progress towards their window for contention. Therefore, to estimate the value of a given pick in the draft, we want to determine its impact on any given team over the next three seasons.\footnote{While not all teams are rebuilding, contending teams benefit from valuing their young talent on a three-year time frame, as this includes the player's time on their rookie contract before they could hit the open-market and sign elsewhere.}

\section{Value\,Added\,and\,Estimated Wins\,Added}

To achieve the goal in the introduction, we will utilize two stats: Value Added (VA) and Estimated Wins Added (EWA). VA represents the estimated number of additional points a player contributes to a team's season compared to the number of points a generic replacement player would contribute. VA is calculated using the equation below with three key stats: minutes played (MP), player efficiency rating (PER), and position replacement level (PRL).

\begin{align*}
    VA &= \frac{MP \, \times (PER - PRL)}{67}
\end{align*}

Minutes played is simply the number of minutes of play a player has recorded, PER is an overall rating of a player's per-minute statistical production, and PRL is a constant, depending on position, that represents what a typical replacement player would produce.

Once a player's value added is calculated, we can then determine a player's Estimated Wins Added (EWA). EWA is similar to value added, but represents the estimated number of additional wins a player contributes to a team's season compared to a replacement player. This is calculated by dividing a player's value added by 30, as it has been determined that a value added of 30 corresponds to contributing 1 win \cite{VA}.

\section{Results}

Now that we know how to calculate EWA, we must do this for each player drafted at each position in the draft, starting from 1980 and going until 2016. This ensures that we have a large enough sample size of players to represent each pick. Once we determine each player's EWA at a certain pick, we take the average to determine the EWA of that pick in the draft. Doing this for each pick 1-60, we get the following graph, as displayed in Figure 1.

\begin{figure}
  \centering
  \includegraphics[width=0.5\textwidth]{figures/graph.png}
  \caption{EWA for each draft pick, 1-60}
\end{figure}

Notice how the relation between the pick number and EWA isn't exactly linear. The difference in value between the 5th overall pick and the 10th overall pick is much larger compared to the difference 25th overall pick and the 30th overall pick. Historically, the top few picks in each draft contain franchise-altering talent who account for a large share of total wins generated across their draft class. However, once you move past the early lottery picks, the gap in expected performance narrows significantly.

Another thing to note is how the regression line estimates that a later pick like the 45th overall pick could be more valuable than some earlier picks like those in the 20s. In modern-day front-offices, most people trust the numbers, understanding that the best players are more often those that the numbers support. However, there are some instances where this isn't the case.

For example, an injury-prone player may put up generational numbers when they're healthy, but having their young-talent constantly off the court is a large risk to inherit. Therefore, injury-prone players fall much later than where their numbers project. Another instance of this phenomenon could be players that come from different countries or smaller universities. Their stats may show that they have superstar potential, but one might question whether that was a consequence of their competition. Would the same be true under the immense pressure of professional sports? Yet, over a large sample size, these factors even each other out and result in a similar value for these range of picks.

\section{Application:\,Trading Draft Picks}

In the NBA, it is very common to see different teams trading draft picks with one another in an attempt to gain more value for their team. With the level of unpredictability that can occur in the draft, it's very difficult to determine whether a proposed trade is in the team's best interest. However, now that we have an estimate of how much production each pick brings, we can use that to discover whether a trade brings us more value than we're giving up, or vice versa.

To do this, we simply add up the Estimated Wins Added of each pick we are giving away and each pick we're receiving. If the EWA of the picks we're receiving is greater than the EWA of the picks we're giving away, this indicates that the trade is in our best interest and we should accept it. On the other hand, if the opposite is true, we should decline the trade and retain the value we currently possess.

\section*{Conclusion}

Draft picks are among the most valuable assets in the NBA, yet it's nearly impossible to assign values to each pick due to the uncertainty of future prospect performance. However, using historical data and calculating each drafted player's Estimated Wins Added (EWA) over their next three seasons, we were able to illustrate the nonlinear relationship between each pick in the draft and its corresponding value.

The most prevalent application of this information was simulating trade proposals involving draft picks. Based on the sum of the Estimated Wins Added for each pick involved, it became easy to determine whether a trade was in a team's best interest to accept or decline. In summary, this information allows NBA front offices to make more informed decisions regarding their young talent and the future of their franchise, setting them up for success.

\begin{thebibliography}{9}
\bibitem{Rebuild} Eric Pincus (2023), \emph{Where NBA Franchises Fit in the Team Building Life Cycle}, \url{https://sportsbusinessclassroom.com/where-nba-franchises-fit-in-the-team-building-life-cycle/}
\bibitem{VA}Captain Calculator, \emph{VA and EWA Calculator}, \url{https://captaincalculator.com/sports/basketball/value-added/}
\end{thebibliography}


\end{document}
