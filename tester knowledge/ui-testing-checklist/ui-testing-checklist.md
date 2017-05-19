# UI Testing Checklist

UI단에서 테스트 고려해봐야 할 사항들을 정리한 문서(word)이다.(원본출처는 파악중)

아래와 같은 이슈로 중요한 기능이 다르게 동작하거나 할 수 있으므로

테스트케이스 작성시 고려해 보아야 한다.

또 다른 체크리스트나 최신환경에서 고려해할 사항이 정리되있다면 추가 작성한다.

문서를 참고해 체크리스트를 간단하게 엑셀(xls)로 작성해 보았다.



아래는 문서의 내용이다.



## Interesting Strings, Numbers, Data Attacks, and More

## Strings

· Minimum allowable length

· Minimum allowable length – 1

· Maximum allowable length

· Minimum allowable length + 1

· Long strings (255, 256, 257, 1000, 1024, 2000, 2048 or more characters)

· Accented Chars (àáâãäåçèéêëìíîðñòôõöö, etc.)

· Common Delimiters and Special Characters ( “ ‘ ` | / \ , ; : & < > ^ * ? Tab )

· Leave Blank

· Single Space

· Multiple Spaces

· Leading Spaces

· SQL Injection ( ‘select * from customer )

· HTML/Java injection:

o Size 10

o

· GB18030

o Meng: ᡒᡓᡔᡕᡖᡗᡘᡙᡚᡛ

o Wei: ږڗژڙښڛڜڝڞڟ

o Yi: ꁿꂀꂁꂂꂃꂄꂅꂆꂇꂈ

o Zang: ꄟꄠꄡꄢꄣꄤꄥꄦꄧꄨ

## Numbers

· Minimum allowable value

· Minimum allowable value – 1

· Maximum allowable value

· Minimum allowable value + 1

· 0

· -1

· 32768 (215)

· 32769 (215 + 1)

· 65536 (216)

· 65537 (216 + 1)

· 2147483648 (231)

· 2147483649 (231 + 1)

· 4294967296 (232)

· 4294967297 (232 + 1)

· Negative

· Decimal (0.0001)

· With Commas (1,234,567)

· European Style (1.234.567,89)

##  

## Paths/Files

#### Opening/Editing Existing File

· Long file names/paths (>255 chars)

· Special characters in file name/path (space * ? / \ | < > , . ( ) [ ] { } ; : ‘ “ ! @ # $ % ^ &)

· File does not exist

· File is write- protected

· File is locked

· File is corrupted

· Non-local locations (http, ftp, OneDrive, GoogleDocs, Azure, etc)

· File is on another OS (e.g. Mac files have an extra Resource that Windows apps may not understand)

#### Creating New File

· Long file names/paths (>255 chars)

· Special characters in file name/path (space * ? / \ | < > , . ( ) [ ] { } ; : ‘ “ ! @ # $ % ^ &)

· File already exists

· No disk space left to create the file

· File crosses a disk sector (is this even still a valid test case)

 

## Time and Date

· Different Formats (June 5, 2001; 06/05/2001; 06/05/01; 06-05-01; 6/5/2001 12:34)

o If testing in a browser, change your language pack.

o Verify display format is consistent across all screens

· Time difference between machines

· Crossing time zones

· Leap days

· Always invalid days (February 30, September 31)

· Feb 29 in non-leap years

· Daylight savings changeover

## Web Site Navigation

· Back button (watch for ‘Expired’ messages and double-posted transactions)

· Refresh

· Bookmark the URL. Select Bookmark when logged out

· Change the URL (change/remove parameters to access unauthorized info)

· Multiple browser instances open

· Different browsers (Chrome, FireFox, mobile, etc.)

## Browser Preferences

· JavaScript off

· Cookies off

· Resize browser window

· Change font-size preferences

· Change language pack

· Change browser zoom settings (125%, 150%, etc.)

Look and Feel

· Fonts/sizes/colors/casing are consistent across all similar screens in the UI

· Icons/Verbiage for similar functionality (Add, Delete, Search, etc.) are consistent across the UI

· Different monitor resolutions

· Running OS in High Contrast mode

· Tab order

Domain-Specific Rules

· Invalid IP address: (999.999.999.999, 1.1.1, etc.)

· Invalid email address: (no “@”, no “.”, space, etc.)

· Invalid age: (-1, 1000)

Other Cases

· Required fields (are they really required?)

· Field widths (e.g. the LastName field should be longer than the FirstName field)

· Tooltips?

· Combo Boxes/Dropdown values make sense

· Appropriate error messages for incorrect values