# Blocking vs Non-blocking, Sync vs Async



#### Blocking

application 실행시 대기 큐에 들어가면서 system call이 완료된 후에 응답을 보냄

#### Non-Blocking

application 실행시 대기 큐에 들어가지 않고 실행 여부와 관계없이 바로 응답을 보냄

#### Synchronous

작업을 요청한 후 해당 작업의 결과가 나올 때까지 기다린 후 처리하는 것. system call의 완료를 기다림

#### Asynchronous

작업을 요청한 후 딴 일을 하다가 해당 작업이 완료되면 완료됨을 통지받고 그에 따른 작업을 처리. system call의 완료를 기다리지 않음

#### Synchronous vs Blocking

시스템의 반환을 기다리는 동안 대기 큐에 머무는 것이 필수가 아니면 synchronous

시스템의 반환을 기다리는 동안 대기 큐에 머무는 것이 필수이면 blocking

#### Asynchronous vs Non-blocking

system call이 반환될 때 데이터와 함께 반환될 경우 non-blocking

system call이 반환될 때 데이터와 함께 반환되지 않는 경우 asynchronous



|                                     | Synchronous | Blocking | Asynchronous | Non-blocking |
| ----------------------------------- | ----------- | -------- | ------------ | ------------ |
| system call의 완료를 기다리는가     | O           | O        |              |              |
| 실행여부와 관계없이 즉시 반환되는가 |             |          | O            | O            |
| 데이터와 함께 반환되는가            | O           | O        |              | O            |
| 대기큐에 기다리는가                 |             | O        |              |              |



#### Reference

* https://asfirstalways.tistory.com/348
* https://www.slideshare.net/unitimes/sync-asyncblockingnonblockingio