# AWS re:Invent 2023 Tech Talk on Building Observability to Increase Resiliency (COP343): [link](https://www.youtube.com/watch?v=MARiKxvrdmc&ab_channel=AWSEvents)

## 1. Diagnose Issues:
- use dimensionality(attributes like website, webpage, api, instances, AZ etc) to compute the right metrics(measurements like latency, error, request, etc).
- set alarms at correct dimensionality and metrics so that it triggers a observability notification in case of outage
- combine many alarms signals together to avoid fatigue or noise sometime. It becomes important to create the composite alarm and alarm tree becomes important
- Measure things which can fail separately separately
- find patterns in high cardinality metrics
- navigate distributed system via tracing

## 2. 4 failure modes:
### Bad dependency
- propagate the incoming trace context to every outbound client call you make to every dependency
- enable collection of trace segment from all services and from your apps
- user service maps derived from trace to triangulate the failing dependency during incidents

### bad component:
- Health checks - Split key application health metrics on separate dimensions for each infrastructure boundary like ec2, AZ, etc.
- Find and alarms on the poorest part of your infrastructure using metrics 

### bad deployment:
  - In case of issue rollback first, ask question later
  - add code revision as a dimensionality to metrics
  - alarms based on the the code revision
  - rollback all type of changes automatically to minimise time to recover or mitigate
  - combine all alarms to composite alarm to rollback faster
  - split key application health metrics on logical boundaries like code revision id to minimise time to detect bad changes

### traffic spike: 
- emit logs that are rich with data so that you can cut your metrics on many dimensions
- record and analyse high cardinality metrics like per customer request volume
- slice and dice metrics that you didn't materialise up front by writing log insight queries

## 3. uncover hidden issues
### External issues:
- measure from everywhere
- aggregate metrics in customer oriented ways
  - Collect client side click-view stream analytics using tools like mixpanel
- compare synthetic workloads metrics with real workload metrics continuously

### Mis-attributed faults: Code bugs etc.
- how many customers suddenly see error that are categoried as their fault, it may actually be our fault.
- calculate metrics like percent of customer instead of percent of request
- Metric dimensionality & cardinality = no of customer with error / no of customer
- dimensionality at http status code: client faults(4xx) vs server faults (5xx)

  
## 4. Prevent future issues
- autoscaling of everything to react quickly to changes in load and maintain health head room
- measure the utilisation of everything from cpu to thread pools to quotas - create dashboard and alarms
- Perf testing: game days(drills) just like production
  - properties of good game days (reasoned, realistic, regular, controlled)
  - regularly perform controlled experiments of failure mode by using fault injection systems
  - replicate production observability into test environment
  - verify behaviour of metrics, alarms, dashboards, logs, etc
  - add new instrumentation, metric alarms after every game day