## 데이터 바인딩이란? (Data Binding) 

UI요소(View)와 데이터/로직(Model/ViewModel) 사이에 데이터가 자동으로 오가도록 연결 

-Source(원본) : 바인딩할 데이터를 갖고 있는 객체, ViewModel의 property 
예) public string Name {get;set;} 

-Target(대상) : 값을 표시하거나 입력받는 UI컨트롤의 속성  
예) TextBox.Text , ItemsControl.ItemsSource , Slider.Value 

-Binding(연결) : XAML의 {Binding ... } 구문 또는 코드 비하인드에서 선언 
누구의 어떤 property를 연결할지 어떤 방향(Mode)로 동작할지, 언제 업데이트 할지 설정 

-DataContext : View에서 바인딩의 기본 Source로 사용할 객체를 지정 
Window.DataContext = new MainViewModel() 또는 <Window.DataContext> 

