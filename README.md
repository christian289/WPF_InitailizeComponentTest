# WPF_InitailizeComponentTest

이 소스는 WPF의 Visual 초기화 조건을 알아보는 테스트 소스입니다.
이 저장소는 아래와 같이 사용합니다.

## 수행방법

1. 소스를 클론합니다.

2. 각각 .NET 5, .NET Core 3.1, .NET Framework 4.8로 생성된 프로젝트를 Debug로 빌드합니다. (Release도 상관은 없습니다.)

3. 아래 파일을 확인합니다.
    - 저장소 경로\WPF_InitailizeComponentTest\WpfInitializeTestDotnet5\obj\Debug\net5.0-windows\App.g.i.cs
    - 저장소 경로\WPF_InitailizeComponentTest\WpfInitializeTestDotnetCore31\obj\Debug\netcoreapp3.1\App.g.i.cs
    - 저장소 경로\WPF_InitailizeComponentTest\WpfInitializeTestDotnetFramework48\obj\Debug\App.g.i.cs

4. 각각 파일을 열고 InitializeComponent() 메서드가 만들어지고, Main 함수에서 InitializeComponent() 메서드를 호출하는지 확인합니다.

5. 각각 .NET 5, .NET Core 3.1, .NET Framework 4.8로 생성된 프로젝트의 App.xaml에서 StartUpUri를 제거합니다.

6. 2번과 3번을 수행합니다.

7. InitializeComponent() 메서드가 존재하지 않고, Main에서도 호출하지 않는 것을 확인합니다.

8. 세 프로젝트에 각각 ViewModelLocator 클래스가 있는지 확인하고, 없으면 생성합니다. (클래스는 비어있어도 됩니다.)

9. 세 프로젝트의 App.xaml에 ViewModelLocator를 정적리소스로 선언합니다.

10. 2번과 3번을 수행합니다.

11. 7번을 수행합니다.

12. 아래 코드 조각을 App.xaml에 추가합니다.

```cs
<Style TargetType="Window">
    <Setter Property="FontSize" Value="28" />
</Style>
```

13. 2번과 3번을 수행합니다.

14. 4번을 수행합니다.

## 결론

WPF에서 InitializeComponent() 메서드를 생성하기 위한 조건은 아래 조건 중에서 1가지만 해당되면 됩니다.

- App.xaml에 Startup 이벤트 추가
- App.xaml에 StartupUri 속성 추가
- App.xaml에 Visual에 관련된 리소스 추가

따라서 App.xaml에 __Visual과 무관한 순수한 C# 클래스인 리소스만 추가될 경우 InitializeComponent() 메서드는 생성되지 않습니다.__

__InitializeComponent() 를 호출해야만 App.xaml의 정적 리소스가 생성됩니다.__
