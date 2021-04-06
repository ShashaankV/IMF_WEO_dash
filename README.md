# IMF_WEO_dash
Outlier interactive plot for IMF WEO hackathon

Example using Plotly's Dash library for making a simple but IMHO very useful dashboard. Purpose is to plot actual vs predicted values. General use to assess any type of forecast (predictive) model. Particularly useful for IMF-WEO (see below) where the model is a complex human-guided algorithm. Outliers are defined as x sigma from robust linear regression line. (Future work - clean up code, annotations, replace * with np, etc., and outlier specifications.)

#Outlier (goodness of fit) dashboard

Display predicted vs actual index. Purpose: interactive visualization to easily identify bad predictions that can be used by user to improve model.

##Motivation - IMF WEO Hackathon Generated for the International Monetary Fund 2018 data visualization 2 hour hackathon. The goal was to make an insightful product for the World Economic Outlook report (WEO) (more below). Notably forecasts made by IMF go through a complex process between country teams and aggregated adjustments. We focused on a tool that assessed the country-level and aggregate predictions. The product was the design of Michelle C Mandolia, Benjamin P Cohn, and Shashaank Vattikuti.

Our guideline:

choose one (or few) useful metrics - something that is easy to visualize and gives insight
use an open-source type programmatic platform with large buy-in and support - we chose Plotly's Dash, no reason to limit clients by unnecessary license fees
Chloropleth - the visualization we avoided

Chloropleths - We were setup for this and pretty much all teams chose these. It is an obvious choice for data with geographic features. However, there was no strong reason to expect geographic continuity at this resolution (unlike a pandemic model, see our covid project).
A different network structure may be useful such as group countries by known shared economic ties (or some cluster analysis). This was not clear at the outset.

Why goodness-of-fit?

extremely simple but powerful tool - plot actual vs predicted index
the visualization gives a quick view of how the model does overall and where (what countries) did it fail on
it is agnostic to the model details; can be used for any kind of quantitative models, modeling
interactive tool - hover (lasso-tool, click, etc.) on single or sets of points to get more info on them, adjust data filters to see patterns (like time from report to actual to see how prediction quality changes with time-out), scan data fitlers to see robustness (example, does outlier country stay as outlier across time-outs, maybe this gives more reason for further investigation)
Main features:

Aggregate metrics - intercept and slope of linear regression model
Outlier country estimates - used a robust regression (reduces outlier effects), then tag outliers based on chi-squared analysis of country residual from robust regression line

##About world economic outlook (WEO) ###What is the International Monetary Fund?

(from Wiki: https://en.wikipedia.org/wiki/International_Monetary_Fund)

"Formed in 1944 ,started in 27 November 1945,7 at the Bretton Woods Conference primarily by the ideas of Harry Dexter White and John Maynard Keynes,8 it came into formal existence in 1945 with 29 member countries and the goal of reconstructing the international monetary system. It now plays a central role in the management of balance of payments difficulties and international financial crises.9 Countries contribute funds to a pool through a quota system from which countries experiencing balance of payments problems can borrow money. As of 2016, the fund had XDR 477 billion (about US$667 billion).10. ... consisting of 190 countries working to foster global monetary cooperation, secure financial stability, facilitate international trade, promote high employment and sustainable economic growth, and reduce poverty around the world while periodically depending on the World Bank for its resources.1"

###Forecasts IMF-WEO about forecasts( analyses of global economic developments during the near and medium term.)

Data is sourced from the the World Economic Outlook (WEO) database. (Data is in ./data/ from the hackathon, using publicly available data from IMF. Data is dated from 2018 competition year. Updated data needs to be reformatted for use, pending clarification from IMF.) 

This "is created during the biannual WEO (IMF) exercise, which begins in January and June of each year and results in the April and September/October WEO publication. A Survey by the IMF staff usually published twice a year. It presents IMF staff economists' analyses of global economic developments during the near and medium term."
(I forget if near and medium term were defined. One objective of our tool was to make this modifiable by 6 month periods (i.e. 6, 12, 18, ... months out).

"The IMF’s World Economic Outlook uses a “bottom-up” approach in producing its forecasts; that is, country teams within the IMF generate projections for individual countries. These are then aggregated, and through a series of iterations where the aggregates feed back into individual countries’ forecasts, forecasts converge to the projections reported in the WEO.

Because forecasts are made by the individual country teams, the methodology can vary from country to country and series to series depending on many factors."
