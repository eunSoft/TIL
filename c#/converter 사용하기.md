Person 객체의 Gender 프로퍼티를 bool으로 관리했을 경우, 그대로 바인딩하면 true/false로 view에 표시된다.
  이를 대신하여 문자로 true면 "여자" false면 "남자"로 표시하기위해 IValueConverter를 사용했다.


## 프로젝트에 Converters 폴더를 만들고
  ```using System;
using System.Collections.Generic;
using System.Globalization;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Data;

namespace wpf1.Converters
{
    /// <summary>
    /// bool -> "여자"/"남자" 문자열로 변환해주는 컨버터
    /// </summary>
    public class GenderToStringConverter : IValueConverter
    {
        public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
        {
            if (value is bool isFemale)
                return isFemale ? "여자" : "남자";
            return "알 수 없음";
        }

        public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
        {
            if(value is string s)
            {
                return s == "여자";
            }
            throw new NotSupportedException();
        }
    }
}
```

`IvalueConverter`를 상속하는 `GenderToStringConverter` 클래스를 만들어주었다.
`Convert` 메서드와 `ConvertBack`메서드를 오버라이딩 해줬다. `ConvertBack` 메서드는 양방향 전환을 위한 것으로 필요하지 않다면 예외처리만 남겨둔다.

## xaml에 컨버터 사용을 위해 등록한다.
   MainWindow.xaml 최 상단에 xaml 네임스페이스를 추가해준다 xmlns:conv="clr-namespace:wpf1.Converters
   리소스에 컨버터 선언 후 key 값을 지정한다.
   <Window.Resources>
  <!-- GenderToStringConverter를 리소스로 등록 -->
  <conv:GenderToStringConverter x:Key="GenderConverter"/>
  </Window.Resources>

  바인딩 시에 컨버터 속성에 추가해주면 된다.
  TextBlock Text="{Binding SelectedPerson.Gender, Converter={StaticResource GenderConverter}}"

   
