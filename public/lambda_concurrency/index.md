# Lambda并发测试


<!--more-->


## 并发的场景

怎么体验Lambda的优点。
我做了两个简单的函数，一个只打印日志，一个增加了2s的Sleep
```
    @Override
    public Object handleRequest(APIGatewayProxyRequestEvent input, Context context) {
        logger.info("ApiGatewayRequestHandler: " + input.getBody());
        return new APIGatewayProxyResponseEvent().withBody("Hi " + input.getBody()).withStatusCode(200);
    }
```

```
@Override
    public Object handleRequest(APIGatewayProxyRequestEvent input, Context context) {
        logger.info("ApiGatewayParallelRequestHandler: " + input.getBody());
        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            // TODO Auto-generated catch block
            e.printStackTrace();
        }
        logger.info("ApiGatewayParallelRequestHandler: after");

        return new APIGatewayProxyResponseEvent().withBody("Hi " + input.getBody()).withStatusCode(200);
    }
```

## 本地调用
启动10个线程，分别调用两个函数20次，我们观察下，两个函数会有什么变化。

## 结果

```
14:53:18.770 [ForkJoinPool.commonPool-worker-9] INFO com.snack.learning.lambda.snacklambda.SnackLambdaApplication - {"statusCode":200,"body":"Hi null"}
14:53:18.770 [main] INFO com.snack.learning.lambda.snacklambda.SnackLambdaApplication - {"statusCode":200,"body":"Hi null"}
14:53:18.770 [ForkJoinPool.commonPool-worker-11] INFO com.snack.learning.lambda.snacklambda.SnackLambdaApplication - {"statusCode":200,"body":"Hi null"}
14:53:18.776 [ForkJoinPool.commonPool-worker-2] INFO com.snack.learning.lambda.snacklambda.SnackLambdaApplication - {"statusCode":200,"body":"Hi null"}
14:53:18.897 [ForkJoinPool.commonPool-worker-13] INFO com.snack.learning.lambda.snacklambda.SnackLambdaApplication - {"statusCode":200,"body":"Hi null"}
14:53:18.909 [ForkJoinPool.commonPool-worker-10] INFO com.snack.learning.lambda.snacklambda.SnackLambdaApplication - {"statusCode":200,"body":"Hi null"}
14:53:18.916 [ForkJoinPool.commonPool-worker-1] INFO com.snack.learning.lambda.snacklambda.SnackLambdaApplication - {"statusCode":200,"body":"Hi null"}
14:53:18.928 [ForkJoinPool.commonPool-worker-15] INFO com.snack.learning.lambda.snacklambda.SnackLambdaApplication - {"statusCode":200,"body":"Hi null"}
14:53:18.978 [ForkJoinPool.commonPool-worker-6] INFO com.snack.learning.lambda.snacklambda.SnackLambdaApplication - {"statusCode":200,"body":"Hi null"}
14:53:19.015 [ForkJoinPool.commonPool-worker-9] INFO com.snack.learning.lambda.snacklambda.SnackLambdaApplication - {"statusCode":200,"body":"Hi null"}
14:53:19.020 [ForkJoinPool.commonPool-worker-2] INFO com.snack.learning.lambda.snacklambda.SnackLambdaApplication - {"statusCode":200,"body":"Hi null"}
14:53:19.023 [main] INFO com.snack.learning.lambda.snacklambda.SnackLambdaApplication - {"statusCode":200,"body":"Hi null"}
14:53:19.025 [ForkJoinPool.commonPool-worker-11] INFO com.snack.learning.lambda.snacklambda.SnackLambdaApplication - {"statusCode":200,"body":"Hi null"}
14:53:19.121 [ForkJoinPool.commonPool-worker-8] INFO com.snack.learning.lambda.snacklambda.SnackLambdaApplication - {"statusCode":200,"body":"Hi null"}
14:53:19.136 [ForkJoinPool.commonPool-worker-13] INFO com.snack.learning.lambda.snacklambda.SnackLambdaApplication - {"statusCode":200,"body":"Hi null"}
14:53:19.143 [ForkJoinPool.commonPool-worker-10] INFO com.snack.learning.lambda.snacklambda.SnackLambdaApplication - {"statusCode":200,"body":"Hi null"}
14:53:19.167 [ForkJoinPool.commonPool-worker-1] INFO com.snack.learning.lambda.snacklambda.SnackLambdaApplication - {"statusCode":200,"body":"Hi null"}
14:53:19.173 [ForkJoinPool.commonPool-worker-15] INFO com.snack.learning.lambda.snacklambda.SnackLambdaApplication - {"statusCode":200,"body":"Hi null"}
14:53:19.224 [ForkJoinPool.commonPool-worker-4] INFO com.snack.learning.lambda.snacklambda.SnackLambdaApplication - {"statusCode":200,"body":"Hi null"}
```
总时间，大概0.5秒，在AWS监控台上，看使用了8个并发实例



## 代码参照
你可以通过 https://github.com/snack8310/snacklambda 下载源代码

