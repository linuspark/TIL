# Active Object Pattern

액티브 오브젝트 패턴은 커맨드 패턴의 응용 방식이다. 이 패턴은 다중 제어 스레드(Thread) 구현을 위한 기법으로 스레드 간의 비동기적인 함수 호출을 객체 지향적으로 구현한 패턴이라고 할 수 있다. 

이 패턴의 기본적인 아이디어는 Command 객체를 연결리스트로 들고 있는 객체(이하 Active Object)가 있고 이 객체에 새로운 명령을 추가(Command 객체를 추가)하거나 들고 있는 명령(Command 객체)을 하나씩 실행하면서 제거할 수 있다. 

여기까지는 뭔가 심플해 보인다. 하지만 명령(Command 객체) 중 하나의 역할이 자기 자신을 복제하여 다시 Active Object 에 추가하는 내용의 명령이라면, Active Object 의 "명령 실행"은 끝나지 않을 것 이다. 바로 이런 방식을 이용하여 다중 스레드를 제어할 수 있다.

# 간단한 예시

```csharp
interface ICommand{
	public void execute();
}

public class ActiveObjectEngine {
	List<ICommand> itsCommands = new List<ICommands>();

	public void AddCommand(ICommand cmd){
		itsCommands.Add(cmd);
	}

	public void run(){
		while (its.Commands.Count != 0){
			ICommand cmd = itsCommands.First();
			itsCommands.RemoveAt(0)
			cmd.excute();
		}
}

public class SleepCommand: ICommand {
	private ActiveObjectEngine _engine;
	private ICommand _wakeUpCommand;
	private long _sleepTime;
	private long _startTime;
	private bool _isStarted = false;

	public SleepCommand(long milliseconds, ActiveObjectEngine e, ICommand wakeUpCommand){
		this._sleepTime = milliseconds;
		this._engine = e;
		this._wakeUpCommand = wakeUpCommand;
	}

	public void execute(){
		long currentTime = time.now();
		if (!this._isStarted){
			this._isStarted = true;
			this._startTime = currentTime;
			this._engine.AddCommand(this);
		} else if ((currentTime - this._startedTime) < this._sleepTime){
			this._engine.AddCommand(this);
		} else {
			this._engine.AddCommand(this._wakeUpCommand);
		}
	}
}

public class TestExecuteCommand: ICommand {
	public void execute(){
		System.Console.WriteLine("Executed");
	}
}

public static class Main{
	public static void main(String args[]){
		ICommand wakeUp = new TestExecuteCommand();
		ActiveObjectEngine engine = new ActiveObjectEngine();
		SleepCommand sleepCommand = new SleepCommand(1000, engine, wakeUp);
		engine.run();
	}
}
```

SleepCommand는 초기에 설정한 일정 시간 동안은 자기 자신을 Active Engine에 넣으면서 동작 하다가 일정 시간이 지나면 미리 설정한 Command를 Active Engine에 넣는다. Active Engine에는 계속해서 Sleep Command가 입력되면서 시간을 기다리다가 일정 시간 후에 미리 설정한 Command를 실행하게 된다.

# 결론

이런 종류의 스레드는 각 Command 인스턴트가 다음 Command 인스턴스의 실행이 가능하기 전에 완료되기 때문에 RTC(Run-to-Completion) 테스크라고 불린다. RTC라는 이름이 뜻하는 것은 Command 인스턴스가 블록하지 않는다는 것 이다.

Command 인스턴스가 모두 완료될 때 까지 실행된다. 라는 이야기는 Command 인스턴스 들이 RTC라는 모두 같은 런타임 스택을 공유한다는 말이다. 전통적인 스레드와는 다르게  RTC에서는 별도의 런타임 스레드를 정의하거나 할당하지 않아도 된다. 이런 이점은 스레드가 많이 실행되어야 하거나 메모리가 제한된 시스템에서 강력한 이점이다. 

---

참고. 로버트C마틴. 클린 소프트웨어 애자일 원칙과 패턴 그리고 실천 방법 (이용원, 김정민, 정지호 옮김)
