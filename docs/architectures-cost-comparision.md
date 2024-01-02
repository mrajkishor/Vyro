![image](https://github.com/mrajkishor/Vyro/assets/148688864/1a15ad28-c0e7-475d-b0cd-71f6b190f7e2)

The graph illustrates the cost comparison between AWS Lambda (Serverless) and Spring Boot microservices hosted on EC2, across different traffic volumes (measured in millions of requests per day).

From the graph, we can observe the following trends:

1. **AWS Lambda Cost**: The cost for AWS Lambda increases linearly with the traffic. This is due to the pricing model of AWS Lambda, which charges per request and per GB-second of compute time. As traffic increases, so does the cost.

2. **Spring Boot Microservices Cost**: The cost for the Spring Boot microservices on EC2 remains constant regardless of the traffic. This flat line represents the fixed cost of running the EC2 instances required for the microservices, based on the assumption of 10 `t3.medium` instances.

3. **Cost Efficiency at Different Traffic Levels**:
   - **Low Traffic**: At lower traffic levels, AWS Lambda tends to be more cost-effective due to its pay-per-use model.
   - **High Traffic**: As traffic increases, the cost of AWS Lambda grows significantly, while the cost for Spring Boot microservices remains constant. Thus, at higher traffic levels, Spring Boot microservices on EC2 become more economical.
