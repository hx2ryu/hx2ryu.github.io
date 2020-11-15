---
title: "Lifecycle [WPF]"
categories: "Windows"
Tags: [wpf, c#]
---

## Lifecycle In WPF

- System.Windows.Application을 상속받은 App class에서 Lifecycle에 접근할 수 있다. (App.xaml.cs)

```C#
public partial class App : Application
{
	protected override void OnActivated(EventArgs e)
	{
		base.OnActivated(e);
	}

	protected override void OnDeactivated(EventArgs e)
	{
		base.OnDeactivated(e);
	}

	protected override void OnExit(ExitEventArgs e)
	{
		base.OnExit(e);
	}

	protected override void OnSessionEnding(SessionEndingCancelEventArgs e)
	{
		base.OnSessionEnding(e);
	}

	protected override void OnStartup(StartupEventArgs e)
	{
		base.OnStartup(e);
	}
}
```



#### 1. Lifecycle

- StartUp: Run method가 호출된 후, Window가 보여지기 전에 발생.

- Activated: 발생되는 시점 2가지 경우.

  - 처음 Window가 보여질 때
  - Focusing이 다른 Window Application에서 넘어 왔을 때

- Deactivated: Focusing이 다른 Window Application으로 넘어 갈 때 발생.

- DispatcherUnhandledException: main thread에서 unhandled exception이 발생할 때 발생.

- SessionEnding: Window session이 끝나는 시점.

  - 윈도우(OS) 종료될 때 혹은 사용자 Log off될 때
  - SessionEndingCancelEventArgs.Cancel property를 이용하여 Shutdown을 취소할 수 있음.

  ```c#
  protected override void OnSessionEnding(SessionEndingCancelEventArgs e)
  {
  	base.OnSessionEnding(e);
  	e.Cancel = true;
  }
  ```

  

- Exit: Run Method가 호출된 후 Shutdown method가 호출 되기 전에 발생.

  - shudown method 호출을 막을 수는 없음.

- Shutdown: Application 종료.

![](/assets/posting_src/knn-1.png/lifecycle_wpf.png)



#### 2. Reference

- [C# Corner: Understanding WPF Application Lifecycle](https://www.c-sharpcorner.com/uploadfile/37db1d/understanding-wpf-application-lifecycle/)

