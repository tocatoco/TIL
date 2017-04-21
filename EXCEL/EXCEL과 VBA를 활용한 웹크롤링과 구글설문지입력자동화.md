# EXCEL과 VBA를 활용한 간단한 웹크롤링과 구글 설문지 입력자동화

간단한 웹크롤링과 웹 브라우저 컨트롤을 통한 설문지 자동 입력 예제




## 간단한 웹크롤링 방법

1. EXCEL 데이터 > 외부데이터 가져오기 > 웹쿼리 선택
2. 필요한 데이터가 있는 테이블 선택 후 가져오는 지 확인

## VBA로 웹브라우져 컨트롤해 설문지 입력

1. 엑셀에 버튼 생성
2. 아래 sur 함수 작성해 버튼에 연결

## 작성코드


```VBA
Dim HTMLDoc As HTMLDocument
Dim MyBrowser As InternetExplorer
 
 
Sub Sur()
 
    '데이터 최신데이터로 모두 새로고침
    ActiveWorkbook.RefreshAll
 
    'Given
    Dim MyHTML_Element As IHTMLElement
    Dim MyURL As String
    On Error GoTo Err_Clear
    MyURL = "http://goo.gl/forms/cKnL8l3S1X"
    Set MyBrowser = New InternetExplorer
    tagetrow = 3
    Dayda = "11"
    
      
    'When
    Do While Worksheets(1).Cells(tagetrow, 2).Value <> ""
 
 
    If (Worksheets(1).Cells(tagetrow, 2) <> "경기가 없습니다.") Then
        MyBrowser.Silent = True
        MyBrowser.navigate MyURL
        MyBrowser.Visible = True
    
        Do
        Loop Until MyBrowser.readyState = READYSTATE_COMPLETE
    
        Set HTMLDoc = MyBrowser.document
        Application.Wait (Now + TimeValue("0:00:01"))
    
        '날짜
        If (Worksheets(1).Cells(tagetrow, 1) <> "") Then
        Dayda = Worksheets(1).Cells(tagetrow, 1)
        End If
        HTMLDoc.all.entry_715337389.Value = Dayda
        Application.Wait (Now + TimeValue("0:00:01"))
 
        '일정
        HTMLDoc.all.entry_662637018.Value = Worksheets(1).Cells(tagetrow, 2)
        Application.Wait (Now + TimeValue("0:00:01"))
    
        '데이터 제출
        For Each MyHTML_Element In HTMLDoc.getElementsByTagName("input")
        If MyHTML_Element.Type = "submit" Then MyHTML_Element.Click: Exit For
        Next
    
        Application.Wait (Now + TimeValue("0:00:01"))
    
        Do
        Loop Until MyBrowser.readyState = READYSTATE_COMPLETE
 
    End If
 
tagetrow = tagetrow + 1
 
Loop
 
MyURL = "https://docs.google.com/spreadsheets/d/13FGvx-I_CzYJqdHWEGmWhH9qQUKnElJDYE_XU-JCcxI/edit?usp=sharing"
        MyBrowser.Silent = True
        MyBrowser.navigate MyURL
        MyBrowser.Visible = True
Application.Wait (Now + TimeValue("0:00:07"))
        
Err_Clear:
   If Err <> 0 Then
   Err.Clear
   Resume Next
   End If
    
'브라우저 종료
MyBrowser.Quit
 
 
End Sub
```

### 작동영상

[![동작영상](http://i.imgur.com/lUIrpHy.png)](https://youtu.be/5RXMKhIFilM "동작영상")