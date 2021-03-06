# Lambda-Architecture-Financial-Risk
The Application of Lambda Architecture to the Financial Risk within the Investment Banking

Purpose

We are in the process of designing an architecture pattern that involves the application of Lambda Architecture to the Financial Risk Calculations in the Investment Banking, utilizing Big Data artifacts.

The banks are looking to reduce risk in the credit business while making more profitable credit and trading decisions. Specifically, they want to identify risk trends within certain years of trading data. For example, measure the risk exposure in a give portfolio by industry, region, credit rating and other parameters. At the macroscopic level they also want to analyze data across market sectors, over a given time horizon to asses risk changes . On top of that, the banks also have to meet new regulatory requirements as a result of recent changes. 

What is this all about

Lambda Architecture is a data-processing architecture designed to handle massive quantities of data by taking advantage of both batch- and stream-processing methods. This approach to architecture attempts to balance latency, throughput, and fault-tolerance by using batch processing to provide comprehensive and accurate views of batch data, while simultaneously using near or real-time stream processing to provide views of online data. The two view outputs may be joined before presentation. The rise of lambda architecture is correlated with the growth of Big Data, real-time analytics, and the drive to mitigate latencies associated with these type of operations.Within the scope of this work I intend to apply Lambda Architecture framework to the Financial Risk calculations in the Investment Banking (IM). I have just started laying down the framework for it.

Goals

Financial Risk is an umbrella term for multiple types of risk associated with financing, including financial transactions that include company loans in risk of default. Risk is a term often used to imply downside risk, meaning the uncertainty of a return and the potential for financial loss.

It is not within the scope of this project to delve into the business aspects of the Financial Risk (I will leave that to the accountants). However, it will be useful to briefly describe the two major components of the Financial Risk; namely Credit Risk and Market Risk.

Credit Risk

Credit risk, also called default risk, is the risk associated with a borrower going into default (not making payments as promised). Thus the Investor losses include lost principal and interest, decreased cash flow, and increased collection costs. An investor can also assume credit risk through direct or indirect use of leverage. For example, an investor may purchase an investment using margin. Or an investment may directly or indirectly use or rely on Repurchase Agreement (repo), forward commitment, or derivative instruments. The risk could also be indirect. A bank may be dealing with another bank who has large exposure to a sovereign nation in default. So there will be a major impact if the aforementioned bank goes down.

Market Risk

Market Risk is normally defined as any shift in the valuation of a portfolio due to a change in any of the following risk categories:

•Equity risk is the risk that stock prices in general or the implied volatility will change.
•Interest rate risk is the risk that interest rates or the implied volatility will change.
•Currency risk is the risk that foreign exchange rates or the implied volatility will change, which affects, for example, the value of an asset held in that currency.
•Commodity risk is the risk that commodity prices or implied volatility will change.

Application of Big Data

You may be wondering where is the strong correlation between Big Data and Market Risks? To manage market risk, banks deploy a number of highly sophisticated mathematical and statistical techniques. Chief among these is value-at-risk (VAR) analysis, which has established itself as the de-facto standard in measuring market risk.
In the wake of the recent banking troubles, there is a growing realisation that relying on VAR using standard techniques is outdated. Regulators have attempted to compensate for some of these limitations, notably through Basel 111, a comprehensive upgrade to the market-risk framework that came in 2011. Some new elements in the framework, such as a requirement to calculate stressed VAR, are driving risk-weighted assets (RWAs) (a bank's assets or off-balance-sheet exposures, weighted according to risk), higher and boosting capital requirements by a factor of two to three. In layman's term this means that a lot of money has to be kept in reserve by banks in case of any issues. As usual banks want to anticipate, be prepared and survive any storm.
So how does this affect IT. IT systems aka risk IT support market risk. Any improvements in market risk modelling must be supported by the corresponding changes in risk IT.
Over many years many trading desks in banks have relied on separate IT systems. These have been developed in silos using a variety of front end development tools and different databases as the back end. The interfaces between these silos have been through what I call bucketing. Every day some run a suite of reports that source data from other systems through crons, .NET, Java, flat files and others, do some calculation and push that data to another silo. Each set-up is optimized to meet the specific needs of itself. While the front-office teams aim for flexibility and finely calibrated pricing models to facilitate agility in rapidly changing markets, the finance function and risk groups are focused on meeting regulatory, accounting, and internal standards. However, as business complexity increases, these separate systems tend to drift apart more and more, and the data flows among them becomes increasingly convoluted. At many banks today, aggregating and verifying market risk across the bank in near real time, let alone real time has become a challenge (and that is an under statement).

With the advent of Big Data lakes banks have started exploring ways to unite these disparate systems. This requires a common data model, some form of in-memory caching for gathering data in some fabric and finally putting data in the Data Lake. They realise the importance of risk aggregation in view of regulatory pressure. They have been looking at:
•Creating a Master Data Model (a standard description of how the bank stores and works with data) to be used throughout the bank, wherever possible. If every business within the bank creates its data in the same way, all the downstream tasks become much simpler.
•Utilising Data Grids (Data Fabric) built on massive Cache relying on available and increasingly in-expensive memory to facilitate the work. Look at this article of mine 
•Deploying Data Lakes. A single trusted source of data, sometimes called a “golden source,” built on Big Data Technology for all the data needs
•Using Real time or Near Real time calculation of risks.

What all this means is that banks have embarked on a variety of vendor technology platforms, analytic models, large data management infrastructure and automated controls. Most of these technologies are new in the market, often open source and rapidly evolving and will need to be mastered and established within the banks's processes and platforms.Hence it is fair to say that Big Data techniques and applications are  providing banks with a feasible solution to extract latent information from the vast volume of data accumulated from all the lines of banks' business. Given the volume of data and the available resources, the banks have now begun to focus on the benefits that Big Data techniques can bring in streamlining current practices, as well as designing new solutions for risk assessment.

Overview

In our attempt to design such system that deals with batch and real time risks, I have adopted a heuristic approach in that I take the generic concept of Lambda Architecture and try to adapt it for general risks scenarios as described above.Based on the axiom that for risk system to be "current", it will require both a batch oriented and near real time response, the key ingredients are:•A high-latency process that computes the 'correct' answer. That will rely on extracts from Data Lake.

•A low-latency process that computes a possibly approximate delta to the last correct answer, possibly expensively (in terms of resourcing). This will be near real time.
•A process that merges the two views. In other words, tries to amalgamate data from both the Data Lake and near real time. This will allow insights based on hot and cold data simultaneously.
•A Real Time Dashboard for data visualisation.
•A conventional Dashboard for Batch data visualisation.•An Alert/notification system.The design will focus on four major functional areas, namely:
•Batch Layer.
•Speed Layer.
•Serving Layer.
•Building Real Time Dashboards.

The major functionalities are described below:

Batch Layer functionalities:
1. Read data from the traditional RDBMS silos using Sqoop, a package or some form of real time replication.
2.Alternatively deploy SAP SRS or GoldenGate.
3.Identify if such set ups are available for the sources.
4.Specify HDFS Hardware and Hadoop core installation.
5.Deliver data to HDFS.6.Establish the design and type of databases and tables on HDFS.7.Work out the frequency of refresh on target files and tables. It could be discrete (once), recurring (refresh it every night/weekend) or accumulating (add new data daily, real time etc).8.Establish end to end scheduling of the jobs.9.Establish monitoring.Speed Layer functionalities:1. Identify the sources of data.2.Design adapter modules for each source.3.Identify the distributed messaging architecture.4.Design deployment patterns for Kafka and its clustering (assuming that we will be using Kafka).5.Design adapters between external sources and Kafka.6.Design patterns for deploying Flume for faster data delivery from Kafka to HDFS7.Design patterns for deploying Spark.8.Spec Spark cluster hardware.9.Spec Spark operations mode.10.Define Spark Streaming parameters for different topics.11.Identify Real time database and tables to write to in Spark.Serving Layer functionalities1. Define an operations mode for the Serving module.2.Identify the interfaces to both Batch and Speed modules.3.Design an architecture for the presentation layer.4.Decide whether a new real time database needed.5.Create and merge views from both Batch and Speed modules.6.Design and build a multi-dimensional visualisation tool/dashboard
