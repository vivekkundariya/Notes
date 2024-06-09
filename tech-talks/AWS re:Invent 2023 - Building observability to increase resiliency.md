# AWS re:Invent 2023 Tech Talk on Building Observability to Increase Resiliency (COP343): [link](https://www.youtube.com/watch?v=MARiKxvrdmc&ab_channel=AWSEvents)

## 1. Diagnose Issues:
<<<<<<< HEAD
- use dimensionality(attributes like website, webpage, api, instances, AZ etc) to compute the right metrics(measurements like latency, error, request, etc).
- set alarms at correct dimensionality and metrics so that it triggers a observability notification in case of outage.
- combine many alarms signals together to avoid fatigue or noise sometime. 
  - It becomes important to create the composite alarm and alarm tree.
- Measure things which can fail separately, separately.
- find patterns in high cardinality metrics.
- navigate distributed system via tracing.

## 2. 4 Dailure modes:
### Bad dependency
- propagate the incoming trace context to every outbound client call you make to every dependency.
- enable collection of trace segment from all services and from your apps.
- user service maps derived from trace to triangulate the failing dependency during incidents.
=======
- Use dimensionality(attributes like website, webpage, api, instances, AZ etc) to compute the right metrics(measurements like latency, error, request, etc).
- Set alarms at correct dimensionality and metrics so that it triggers a observability notification in case of outage.
- Combine many alarms signals together to avoid fatigue or noise sometime. 
  - It becomes important to create the composite alarm and alarm tree.
- Measure things which can fail separately, separately.
- Find patterns in high cardinality metrics.
- Navigate distributed system via tracing.

## 2. 4 Failure modes:
### Bad dependency
- Propagate the incoming trace context to every outbound client call you make to every dependency.
- Enable collection of trace segment from all services and from your apps.
- Use service maps derived from trace to triangulate the failing dependency during incidents.
>>>>>>> 076e2cc (fix typos)

### Bad component:
- Health checks - Split key application health metrics on separate dimensions for each infrastructure boundary like ec2, AZ, etc.
- Find and alarms on the poorest part of your infrastructure using metrics. 

### Bad deployment:
  - In case of issue rollback first, ask question later.
  - Add code revision as a dimensionality to metrics.
  - Alarms based on the code revision.
  - Rollback all type of changes automatically to minimise time to recover or mitigate.
  - Combine all alarms to composite alarm to rollback faster.
  - Split key application health metrics on logical boundaries like code revision id to minimise time to detect bad changes.

### Traffic spike: 
- Emit logs that are rich with data so that you can cut your metrics on many dimensions.
- Record and analyse high cardinality metrics like per customer request volume.
- Slice and dice metrics that you didn't materialise up front by writing log insight queries.

## 3. uncover hidden issues
### External issues:
- Measure from everywhere.
- Aggregate metrics in customer oriented ways.
  - Collect client side click-view stream analytics using tools like mixpanel.
- Compare synthetic workloads metrics with real workload metrics continuously.

### Mis-attributed faults: Code bugs etc.
- How many customers suddenly see error that are categoried as their fault, it may actually be our fault.
- Calculate metrics like percent of customer instead of percent of request.
- Metric dimensionality & cardinality = no of customer with error / no of customer.
- Dimensionality of metrics at http status code: client faults(4xx) vs server faults (5xx).

  
## 4. Prevent future issues
- Autoscaling of everything to react quickly to changes in load and maintain health head room
- Measure the utilisation of everything from cpu to thread pools to quotas - create dashboard and alarms
- Perf testing: game days(drills) just like production.
  - Properties of good game days: reasoned, realistic, regular, controlled.
  - Regularly perform controlled experiments of failure mode by using fault injection systems.
  - Replicate production observability into test environment.
  - Verify behaviour of metrics, alarms, dashboards, logs, etc.
  - Add new instrumentation, metric alarms after every game day.