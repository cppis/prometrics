# prometrics
prometheus metrics example

* create go.mod file:  
  ```bash
  go build
  ./prometrics  
  ```

* check metrics:  
  ```bash
  curl localhost:8080/service?cost=0.2
  curl localhost:8080/metrics | grep myapp
  ```

<br/><br/><br/>

## [Metric types | Prometheus](https://godekdls.github.aio/Prometheus/metric-types/)  
Prometheus 클라이언트 라이브러리는 4가지 핵심 메트릭 유형을 제공합니다.  
Prometheus 서버는 아직 유형 정보를 사용하지 않으며 모든 데이터를 유형이 지정되지 않은 시계열로 병합합니다.  
(이는 향후 변경될 수 있습니다.)

* [Counter](https://prometheus.io/docs/concepts/metric_types/#counter)  
  Counter 는 누적되는 지표로 값이 증가하거나 0으로 리셋하기 위해서는 재시작해야하는 단조 증가 카운터(monotonically increasing counter)입니다.  
  감소할 수 있는 값을 표현할 때에는 사용하면 안됩니다.  

* [Gauge](https://prometheus.io/docs/concepts/metric_types/#gauge)  
  Gauge(게이지)는 임의로 증가, 감소할 수 있는 단일 숫자 값을 나타내는 지표입니다.  
  게이지는 일반적으로 온도 또는 현재 메모리 사용량과 같은 측정값에 사용되지만 동시 요청 수와 같이 증가하거나 감소할 수 있는 "수"에도 사용됩니다.  

* [Histogram](https://prometheus.io/docs/concepts/metric_types/#histogram)  
  Histogram은 관찰(일반적으로 요청 기간 또는 응답 크기와 같은 것)을 샘플링하고 구성 가능한 버킷에서 계산합니다.  
  또 모든 관찰된 값의 합계를 제공합니다.  

  기본 지표 이름이 `<basename>`인 Histogram은 수집하는 동안 여러 시계열(time series)을 노출합니다.  

  * 노출되는 관찰 버킷의 누적 카운터 `<basename>_bucket{le="<upper inclusive bound>"}`   
  * 노출된 모든 관찰된 값의 총합 `<basename>_sum`  
  * 노출된 관찰된 이벤트 수(위의 <basename>_bucket{le="+Inf"}와 동일) `<basename>_count`  

  `histogram_quantile()` 함수를 사용하여 Histogram 또는 Histogram 집계에서 분위수(quantile)를 계산합니다.  
  Histogram은 Apdex 점수를 계산하는 데에도 적합합니다. 버킷에서 작업할 때 Histogram은 누적됩니다.  

* [Summary](https://prometheus.io/docs/concepts/metric_types/#summary)  
  Histogram 과 비슷한 Summary 는 관찰된 값을 샘플링합니다.(일반적으로 요청 기간과 응답 크기처럼) 또 총 관찰 수와 모든 관찰 값의 합계를 제공하지만 슬라이딩 시간 창에서 구성 가능한 분위수를 계산합니다.  

  기본 메트릭 이름이 `<basename>` 인 Summary 는 수집하는 동안 여러 시계열을 노출합니다.

  * 노출된 관찰된 이벤트의 스트리밍 *φ-quantile* (0 ≤ φ ≤ 1) `<basename>{quantile="<φ>"}` 
  * 노출된 모든 관찰된 값의 총합 `<basename>_sum`  
  * 노출된 관찰된 이벤트 수 `<basename>_count`  
 
<br/><br/><br/>

## References  
* [Custom Prometheus Metrics for Apps Running in Kubernetes](https://zhimin-wen.medium.com/custom-prometheus-metrics-for-apps-running-in-kubernetes-498d69ada7aa)  
* [Setup Prometheus Monitoring on Kubernetes using Helm and Prometheus Operator | Part 1](https://www.youtube.com/watch?v=QoDqxm7ybLc)  
* [Metric types | Prometheus](https://prometheus.io/docs/concepts/metric_types/)  
* [HISTOGRAMS AND SUMMARIES | Prometheus](https://prometheus.io/docs/practices/histograms/)  
