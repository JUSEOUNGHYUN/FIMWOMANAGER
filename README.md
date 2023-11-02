# 📛 벽산영동공장 자동화 프로그램
📍 프로젝트 기간 : 2023.05.17 ~ 2023.08.04 (3개월)


# 📌 개요
- 벽산영동공장에서 생산품을 생산할때 컴퓨터 응용프로그램으로 생산품의 생산일정, 규격, 기간, 종류를 날짜 순으로 사용자가 보기 쉽게 WPF DataGrid(표)로 만들어 사용자가 생산계획표을 쉽게 생성,삭제,수정 할 수있도록 구현했습니다.

# 🛠️ 기술 및 도구
<img src="https://img.shields.io/badge/C Sharp-239120?style=flat-square&logo=C Sharp&logoColor=white"/> <img src="https://img.shields.io/badge/Microsoft SQL Server-CC2927?style=flat-square&logo=Microsoft SQL Server&logoColor=white"/> <img src="https://img.shields.io/badge/WPF-40AEF0?style=flat-square&logo=WPF&logoColor=white"/>

# 🎏 기능 구현
- DataGrid Data Binding(MSSQL DB)
- UserControl(Textbox, DatePicker, TimePicker)
- DataGridTemplateColumn.CellEditingTemplate (조회된 DataGrid에서 Remark를 UI에서 직접 수정 가능하고 수정된 데이터가 DB에 저장되는 기능 구현)
- LabelPrint 출력
- DataGrid에 출력된 데이터들을 엑셀에 데이터를 옮기고 저장 (Microsoft.Office.Interop.Excel)
- App.Config Key Data에 따라 Administrator 등급 결정 (AppSettingsReader, WindowsIdentity, ProcessStartInfo)
- TreeView (ObservableCollection)
- delegate (DataPassEventHandler)
- Queue LogMessage로 로그 기록 
- MSSQL Table 분석 후, Data Trigger 관리

### 1. 기본 화면
- 2023.05.15 ~ 2023.05.21에 생산 대기중,생산중,생산완료된 제품들을 DataGrid에 출력

![화면 캡처 2023-11-02 044850](https://github.com/JUSEOUNGHYUN/JUSEOUNGHYUN/assets/80812790/e59764ca-cf24-4eb3-baf6-03262c3e8648)

### 2. UserControl
<p>$\bf{\rm{\color{#5ad7b7}2.1\ Textbox}}$</p>
- 규격코드 등록에서 새로운 제품을 등록하거나 수정할때 생산성을 입력할때
1. 천자리가 넘어가면 ','가 생겨야함
2. 소수점은 3자리 고정
3. 정수 부분을 입력하고 오른쪽 화살표 키를 누르면 소수자리로 이동
4. 정수 자리수는 8자리가 최대
- 이 조건을 모두 충족하기 위해서 따로 UserControl로 Textbox를 구현했습니다.

https://github.com/JUSEOUNGHYUN/JUSEOUNGHYUN/assets/80812790/107f37f2-8adc-4359-8109-49e77921bd77

<p>$\bf{\rm{\color{#5ad7b7}2.2\ DatePicker}}$</p>
1. Year Textbox에서 4자리가 넘어가면 리셋
2. Tab키를 누르면 Year, Month, Day Textbox 순으로 넘어감
3. Month Textbox = 12 이상 입력하면 리셋
4. Day Textbox = 달에 따라 일 입력 적용

https://github.com/JUSEOUNGHYUN/JUSEOUNGHYUN/assets/80812790/7498c8b2-ae1a-4497-aa5f-4b72271edccd

5. DatePicker에 Today Button 생성

https://github.com/JUSEOUNGHYUN/JUSEOUNGHYUN/assets/80812790/af1c3757-562f-42a4-8662-8fef924d6264

<p>$\bf{\rm{\color{#5ad7b7}2.3\ TimePicker}}$</p>

https://github.com/JUSEOUNGHYUN/JUSEOUNGHYUN/assets/80812790/62a9236e-7984-468c-b9cd-8904f8d9d781

### 3. LabelPrint 출력

![LabelPrint](https://github.com/JUSEOUNGHYUN/JUSEOUNGHYUN/assets/80812790/7929c475-1270-4cb6-8b73-9765a8e764b5)

### 4. TreeView (ObservableCollection) 
    public class MenuItem
    {
        public MenuItem()
        {
            this.Items = new ObservableCollection<MenuItem>();
        }
    
        public string Title { get; set; }
    
        public ObservableCollection<MenuItem> Items { get; set; }
    }

https://github.com/JUSEOUNGHYUN/JUSEOUNGHYUN/assets/80812790/d5dfdfed-6911-43cf-951a-e9ca8c49fb23


# 💬 느낀점
- MFC, Winform에서 UI를 개발할때 버튼이나, TextBox 등등 마우스로 생성하고 일일히 정렬 했어야 됐는데 WPF xaml을 사용함으로써 UI의 디자인의 퀄리티가 높아졌고 UI 개발할때 더 쉽게 개발을 할수 있다는걸 알게됐습니다.
- 그리고 일부 테이블의 데이터를 수정하거나, 생성할때 다른 테이블의 데이터가 생성돼었는데 
여기서 Database의 Trigger에 대한 개념과 사용법을 알게됐습니다.
