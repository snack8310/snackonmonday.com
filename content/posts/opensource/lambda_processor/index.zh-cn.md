---
title: "Lambda的线程数"
date: 2022-01-26T14:28:02+08:00
draft: false
---

### Lambda的线程

### 本地
我们部署下面一段代码
```
logger.info("availableProcessors: " + Runtime.getRuntime().availableProcessors());

        IntStream.range(1, 10).parallel().forEach(id->{
            logger.info("Thread: " + Thread.currentThread());
            logger.info("ForkJoinPool Size: " + ForkJoinPool.commonPool().getPoolSize());

            try {
                Thread.sleep(2000);
            } catch (InterruptedException e) {
                // TODO Auto-generated catch block
                e.printStackTrace();
            }
        });
```

我本地cpu是i5，2核线程增强型，所以应该有4个并发线程可以使用。结果也如预期；
```
12:11:08.888 [main] INFO com.snack.learning.threadinlambda.ThreadInLocalApplication - availableProcessors: 4
12:11:09.038 [main] INFO com.snack.learning.threadinlambda.ThreadInLocalApplication - Thread: Thread[main,5,main]
12:11:09.038 [ForkJoinPool.commonPool-worker-1] INFO com.snack.learning.threadinlambda.ThreadInLocalApplication - Thread: Thread[ForkJoinPool.commonPool-worker-1,5,main]
12:11:09.038 [ForkJoinPool.commonPool-worker-1] INFO com.snack.learning.threadinlambda.ThreadInLocalApplication - ForkJoinPool Size: 3
12:11:09.038 [ForkJoinPool.commonPool-worker-2] INFO com.snack.learning.threadinlambda.ThreadInLocalApplication - Thread: Thread[ForkJoinPool.commonPool-worker-2,5,main]
12:11:09.038 [ForkJoinPool.commonPool-worker-2] INFO com.snack.learning.threadinlambda.ThreadInLocalApplication - ForkJoinPool Size: 3
12:11:09.038 [ForkJoinPool.commonPool-worker-3] INFO com.snack.learning.threadinlambda.ThreadInLocalApplication - Thread: Thread[ForkJoinPool.commonPool-worker-3,5,main]
12:11:09.039 [ForkJoinPool.commonPool-worker-3] INFO com.snack.learning.threadinlambda.ThreadInLocalApplication - ForkJoinPool Size: 3
12:11:09.040 [main] INFO com.snack.learning.threadinlambda.ThreadInLocalApplication - ForkJoinPool Size: 3
12:11:11.039 [ForkJoinPool.commonPool-worker-1] INFO com.snack.learning.threadinlambda.ThreadInLocalApplication - Thread: Thread[ForkJoinPool.commonPool-worker-1,5,main]
12:11:11.039 [ForkJoinPool.commonPool-worker-2] INFO com.snack.learning.threadinlambda.ThreadInLocalApplication - Thread: Thread[ForkJoinPool.commonPool-worker-2,5,main]
12:11:11.039 [ForkJoinPool.commonPool-worker-1] INFO com.snack.learning.threadinlambda.ThreadInLocalApplication - ForkJoinPool Size: 3
12:11:11.039 [ForkJoinPool.commonPool-worker-2] INFO com.snack.learning.threadinlambda.ThreadInLocalApplication - ForkJoinPool Size: 3
12:11:11.039 [ForkJoinPool.commonPool-worker-3] INFO com.snack.learning.threadinlambda.ThreadInLocalApplication - Thread: Thread[ForkJoinPool.commonPool-worker-3,5,main]
12:11:11.039 [ForkJoinPool.commonPool-worker-3] INFO com.snack.learning.threadinlambda.ThreadInLocalApplication - ForkJoinPool Size: 3
12:11:11.045 [main] INFO com.snack.learning.threadinlambda.ThreadInLocalApplication - Thread: Thread[main,5,main]
12:11:11.045 [main] INFO com.snack.learning.threadinlambda.ThreadInLocalApplication - ForkJoinPool Size: 3
12:11:13.093 [ForkJoinPool.commonPool-worker-2] INFO com.snack.learning.threadinlambda.ThreadInLocalApplication - Thread: Thread[ForkJoinPool.commonPool-worker-2,5,main]
12:11:13.093 [ForkJoinPool.commonPool-worker-2] INFO com.snack.learning.threadinlambda.ThreadInLocalApplication - ForkJoinPool Size: 3
```

### Lambda 512M版本
把同样的代码，发布到线上

```
2022-01-26T11:37:55.450+08:00	03:37:55.447 [main] INFO com.snack.learning.ThreadInLambda - availableProcessors: 2

2022-01-26T11:37:55.455+08:00	03:37:55.455 [main] INFO com.snack.learning.ThreadInLambda - Thread: Thread[main,5,main]

2022-01-26T11:37:55.455+08:00	03:37:55.455 [main] INFO com.snack.learning.ThreadInLambda - ForkJoinPool Size: 1

2022-01-26T11:37:55.455+08:00	03:37:55.455 [ForkJoinPool.commonPool-worker-1] INFO com.snack.learning.ThreadInLambda - Thread: Thread[ForkJoinPool.commonPool-worker-1,5,main]

2022-01-26T11:37:55.455+08:00	03:37:55.455 [ForkJoinPool.commonPool-worker-1] INFO com.snack.learning.ThreadInLambda - ForkJoinPool Size: 1

2022-01-26T11:37:57.455+08:00	03:37:57.455 [main] INFO com.snack.learning.ThreadInLambda - Thread: Thread[main,5,main]

2022-01-26T11:37:57.456+08:00	03:37:57.455 [main] INFO com.snack.learning.ThreadInLambda - ForkJoinPool Size: 1

2022-01-26T11:37:57.456+08:00	03:37:57.455 [ForkJoinPool.commonPool-worker-1] INFO com.snack.learning.ThreadInLambda - Thread: Thread[ForkJoinPool.commonPool-worker-1,5,main]

2022-01-26T11:37:57.456+08:00	03:37:57.456 [ForkJoinPool.commonPool-worker-1] INFO com.snack.learning.ThreadInLambda - ForkJoinPool Size: 1

2022-01-26T11:37:59.456+08:00	03:37:59.456 [main] INFO com.snack.learning.ThreadInLambda - Thread: Thread[main,5,main]

2022-01-26T11:37:59.456+08:00	03:37:59.456 [main] INFO com.snack.learning.ThreadInLambda - ForkJoinPool Size: 1

2022-01-26T11:37:59.456+08:00	03:37:59.456 [ForkJoinPool.commonPool-worker-1] INFO com.snack.learning.ThreadInLambda - Thread: Thread[ForkJoinPool.commonPool-worker-1,5,main]

2022-01-26T11:37:59.456+08:00	03:37:59.456 [ForkJoinPool.commonPool-worker-1] INFO com.snack.learning.ThreadInLambda - ForkJoinPool Size: 1

2022-01-26T11:38:01.456+08:00	03:38:01.456 [main] INFO com.snack.learning.ThreadInLambda - Thread: Thread[main,5,main]

2022-01-26T11:38:01.456+08:00	03:38:01.456 [ForkJoinPool.commonPool-worker-1] INFO com.snack.learning.ThreadInLambda - Thread: Thread[ForkJoinPool.commonPool-worker-1,5,main]

2022-01-26T11:38:01.456+08:00	03:38:01.456 [ForkJoinPool.commonPool-worker-1] INFO com.snack.learning.ThreadInLambda - ForkJoinPool Size: 1

2022-01-26T11:38:01.456+08:00	03:38:01.456 [main] INFO com.snack.learning.ThreadInLambda - ForkJoinPool Size: 1

2022-01-26T11:38:03.457+08:00	03:38:03.457 [main] INFO com.snack.learning.ThreadInLambda - Thread: Thread[main,5,main]

2022-01-26T11:38:03.457+08:00	03:38:03.457 [main] INFO com.snack.learning.ThreadInLambda - ForkJoinPool Size: 1
```

看到Lambda函数是单核线程增强型，共有2个进程。


### Lambda 2048M版本
我们尝试增加Lambda使用内存数，日志不变。

说明Lambda函数设计，是为了作为单线程任务使用，不想做过于复杂的业务处理。

### 代码参照
你可以通过 https://github.com/snack8310/thread-in-lambda 下载源代码
