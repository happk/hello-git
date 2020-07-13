# PowerShell批量重命名技巧
&emsp;&emsp;若直接選擇**多個檔案**並右鍵重新命名"xxx"時，會以"xxx(1)"、"xxx(2)"......的結果呈現。
<br>因此，使用指令以自訂命名格式。
<br>......**在此前，先記錄下撰寫此文時學到的新玩意**
<br><br>
## Markdown中強制換行、空格
```        
    &emsp;  全型空格
    &ensp;  半型空格
    <br>    換行
```
&emsp;&nbsp加冒號也能空格，不過容易受其他字字寬影響。

## PS的預備知識
PS與CMD相異，多有不互通的語法。例如PS可以使用**pwd**獲取目前路徑，CMD則不行。<br>
而且雖然皆可利用**dir**獲取當前目錄的內容，PS並無**\\a**的參數設定。

## 實際代碼
```powershell
>dir -Recurse| `
>>     Where-Object {$_.Name -match 'epub'} | `
>>       Rename-Item -NewName { $_.Name -replace '\(([0-9])\)','$1'} 
```
* **dir** 表示目錄下的所有內容(包含子目錄本身)。可以以**Get-ChildItem**取代。
* **-Recurse** 表示子目錄下的檔案也會影響。
---
 **where-Object** 篩選物件
 * **-match** 參數表示選取符合者**符合**者

此部分是為了避免Rename-Item掃描到**子資料夾**時報錯。

---
**Rename-Item** 重命名的主體

## 參考資料
[大量自動修改檔名教學與範例](https://officeguide.cc/batch-rename-multiple-files-tutorial-examples/)<br>
[如何大量更改檔名 - iT 邦幫忙](https://ithelp.ithome.com.tw/questions/10047108)<br>
[PowerShell - replace names of all directiories and files in PS - Stack Overflow](https://stackoverflow.com/questions/8518518/replace-names-of-all-directiories-and-files-in-ps)
--講道理這個答主雖然答案正確，但解釋的理由好怪啊<br>
[正規表達式 - JavaScript | MDN](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Guide/Regular_Expressions)