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

        <local:DotTextboxUserControl x:Name="Capacity_TextBox" Height="20" Margin="462,344,84,14" />

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

### 5. Delegate (DataPassEventHandler) 

    pcs.DataPassProdCd += new ProdClassSystem.DataPassProdCdEventHandler(ProdCdReceiveData);

https://github.com/JUSEOUNGHYUN/JUSEOUNGHYUN/assets/80812790/d5dfdfed-6911-43cf-951a-e9ca8c49fb23
