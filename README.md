# Determining effectiveness of a new version of an E-Commerce website using AB Testing

A/B testing (also known as split testing or bucket testing) is a method of comparing two versions of a webpage or app against each other to determine which one performs better. AB testing is essentially an experiment where two or more variants of a page are shown to users at random, and statistical analysis is used to determine which variation performs better for a given conversion goal. 

Using SQL, we analyze the AB Test results available on the [Mode Public Warehouse (login required)](https://app.mode.com/home/pranav_tumkur/data_sources/0a671f65888c) to determine which test has the best effectiveness based on customer response received after completion of the testing.

![images](https://user-images.githubusercontent.com/65482013/84435684-dc802180-ac4f-11ea-8957-936a6dc0c5f6.png)

# AB Testing Conducted

Six tests were carried out on an E-Commerce website, i.e six version of a page were made to test the best page with two test assignments viz. 0 and 1. We are now required to find out the best page version based on 2 parameters:

### View Item Metrics

In this metric, we identify the quantum of views versus the items on which the test was conducted for each of the test assignments. We also calculate and plot the average views per test assignment. In our case, following is the distribution:

| Test Assignment | items | viewed_items | Average views per item |
|-----------------|-------|--------------|------------------------|
| 0               | 1130  | 918          | 1.69                   |
| 1               | 1068  | 890          | 1.74                   |

We can thus say tha test assignment 1 was better as per the View Item Metric.


### Item Order Metrics

In this metric, we identify the quantity of orders made by customers versus the items on which the test was conducted for each of the test assignments.We set a time limit for the validity of the outputs as 30 days, i.e we only cosider orders booked within 30 days after the AB testing as those which were impacted by the website changes. We also plot the Items Ordered versus total items. In our case, following is the distribution:

| Test Assignment | items | ordered_items_30d |
|-----------------|-------|-------------------|
| 0               | 1130  | 341               |
| 1               | 1068  | 319               |

We can thus say tha test assignment 0 was slightly better as per the Item Order Metric..

![Capture1](https://user-images.githubusercontent.com/65482013/84435017-a8583100-ac4e-11ea-9c9d-5a7c37ad786b.PNG)


# Computing the lift and p-value

Using the link: https://thumbtack.github.io/abba/demo/abba.html, we compute the lifts in metrics and the p-values for the binary metrics (30 day order binary and 30 day view binary) using an interval 95% confidence. 

The Lift was just 2.5% and the p-value was 0.2. Such a low p-value indicated that the increase was due to chance. Therefore the increase in views is statistically insignificant. We need more data, i.e we needed to run the AB Test for atleast a week more to get statistically significant results.

