# Task.Run vs Task.Factory.StartNew

## Task.Run

ThreadPool 에서 특정 작업을 실행하기 위한 큐에 넣고 해당 작업에 대한 Task<TResult> 핸들을 반환한다.

## Task.Factory.StartNew

Task를 생성하고 즉시 실행한다.

# Difference

Task.Run 은 .NET Framework 4.5 에서 새로 추가가 되었으며 Task 를 만들고 실행하기 위한 가장 쉬운 방법이다. Task 를 default 설정으로 시작하기 때문이다.

즉, Task.Factory.StartNew 를 보다 쉽게 사용하기 위해 만들어 진 것이 Task.Run 이다.

그럼 Default 설정이 어떤 것인지 보면, Task.Factory.StartNew() 함수는 다음과 같은 형태를 가지고 있다.

```csharp
Task.Factory.StartNew(
	Action<object?> action, // 수행할 작업
	object? state, // 수행할 작업의 인자
	CancellationToken cancelToken, 
	TaskCreationOptions creationOption, 
	TaskScheduler scheduler);
```

action과 state는 수행할 작업과 파라미터이기 때문에 넘어가면 실질적으로 옵션은 TaskCreationOptions 와 TaskScheduler 에 대한 설정이 남는다. Task.Run 을 사용할 경우 Default로 다음과 같은 값이 들어가게 된다.

- TaskCreationOption → DenyChildAttach

    Specifies that any child task that attempts to execute as an attached child task (that is, it is created with the AttachedToParent option) will not be able to attach to the parent task and will execute instead as a detached child task. For more information, see Attached and Detached Child Tasks. - MSDN

    자식 작업이 부모 작업에게 연결되지 않고 독립적으로 수행되도록 하는 옵션이다(Detached child task). 이 옵션과 반대되는 옵션으로는 TaskCreationOptions.AttachedToParent 가 있으며 부모 작업에게 연결된 Task (Attached child task) 가 생성된다.

    Attached Child Task 의 경우, 부모 작업은 자식 작업이 끝날 때 (Complete) 까지 기다리며, 자식의 예외(Exception)를 전파한다. 또한 자식 작업의 Status 에 따라 부모 작업의 Status 가 변한다. Detached Child Task 의 경우 그와 반대이다.

- TaskScheduler → TaskScheduler.Default

    .NET 이 제공하는 기본 TaskScheduler 인스턴스이다. Default와 다른 속성으로는 Current 속성이 있는데 TaskScheduler.Current 의 경우 현재 실행중인 작업과 연결된 TaskScheduler를 가져온다.

# 언제 어떤 것을 사용해야 하는가

기본적으로 compute-bound task, 즉 계산 위주의 작업을 수행할 때에는 Task.Run 을 추천한다. StartNew를 사용하는 경우는 작업이 세분화된 제어가 필요할 때 사용한다. long-running 할 것인지, compute-bound task 인지. 

결론은 작업 내부에서 관리가 필요한 자식 작업을 만들지 않고, 백그라운드에서 가볍게 동작할 작업이라면 Task.Run을, 그렇지 않고 세부 옵션을 적용하고자 할 경우 Task.Factory.StartNew를 사용한다.

이 외에도 Task.Run 의 경우 자식 작업의 예외 (Exception)를 통지 받지 못 한다는 것, StartNew 에서는 async 가 바로 적용되지 않는다는 것(.Unwrap 함수를 사용해야 한다.) 등을 고려해서 사용할 함수를 결정할 수 있다.

# StartNew에서는 async를 사용하지 못 할까

결론부터 말하면 async를 사용할 수는 있다. Unwrap() 을 사용하거나, await await를 사용하면 된다. 

```csharp
var result = await Task.Factory.StartNew(async FunctionA, CancellationToken.None).Unwrap();

var result = await await Task.Factory.StartNew(async FunctionA, CancellationToken.None);
```

이건 Task.Factory.StartNew 가 반환하는 것은 Task<TResult> 이기 때문이다. 만약 StartNew 로 수행하는 작업에 async 를 사용하게 되면 내부 작업의 반환은 Task,  Task<TResult> 가 되게 되고 StartNew로 반환되는 것은 Task<Task<TResult>>가 되어버린다. 때문에 Unwrap을 하거나 await를 두 번 작성해야 하는 것.

참고 - msdn [https://docs.microsoft.com/ko-kr/dotnet/api/system.threading.tasks.task.run?view=net-5.0](https://docs.microsoft.com/ko-kr/dotnet/api/system.threading.tasks.task.run?view=net-5.0)

참고 - [https://ivorycirrus.github.io/TIL/csharp-task-run/](https://ivorycirrus.github.io/TIL/csharp-task-run/)

참고 - [https://devblogs.microsoft.com/pfxteam/task-run-vs-task-factory-startnew/](https://devblogs.microsoft.com/pfxteam/task-run-vs-task-factory-startnew/)