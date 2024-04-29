# API Service

| Category     | SLI | SLO                                                                                                         |
|--------------|-----|-------------------------------------------------------------------------------------------------------------|
| Availability | (Number Successful Requests) / (Total Requests) | 99%                                                                                                         |
| Latency      | 90th percentile of request duration | 90% of requests below 100ms                                                                                 |
| Error Budget | 1-[(1-compliance)/(1-objective)] | Error budget is defined at 20%. This means that 20% of the requests can fail and still be within the budget |
| Throughput   | rate of successful requests per second | 5 RPS indicates the application is functioning                                                              |
