# clean-code-javascript-memo
## 前言
在寫這份 `MEMO` 的當下，已經不知道是我第幾次重新打開 `clean-code` ，並從頭閱讀。但在每次讀完後，都會帶著大部分的認同，中部分的中立，和小部分的不認同，然後就放在一旁。這次希望能結合開發實務上的經驗和個人見解，對每一條內容進行評分，有必要的會進行詳細的文字補充，以整理出屬於自己一套的`整潔`。

🌟 : 認同程度，滿分5

👻 : 實行上的困難程度，滿分5

## 變數

### 使用有意義，並且能正常發音的名稱（便於交流上使用）。

🌟 🌟 🌟 🌟 🌟

👻 👻 👻 👻 👻

在開發實務上，直接面對面的交流溝通是避免不了的。取一個大家方便溝通，並都能有所共識的名字，可以讓合作更愉快。

### 對同類型意義的變數使用相同的名稱。

🌟 🌟 🌟 🌟 🌟

👻 👻 👻 👻

在產品開發上，功能設計面上的耦合是必定存在的。在程式面上，如果是多人合作開發，這塊更考驗的是統整程式的人的功力（要求所有合作開發者都有一定的共識，是幾乎不可能的（吧））。如果不能做到所有細項的命名都保持一致，至少大的分類上要保持一致。

### 對像是固定值的常數，使用具有意義，可被搜索的變數來取代。

🌟 🌟 🌟

👻

概念上與`使用具意義的變數`的規則重疊。但這邊主要是面對那些常數。例如做單位轉換時，就有會很多固定值的使用。對這些值應該要用具意義的變數來取代，一個增加閱讀性，一個是方便做全域搜索。

在這一塊有部分的不認同。生成變數的成本如果不能帶來相對應的價值，在這邊也就是不具備**搜索性**，只會帶來開發上的不便，和閱讀上的冗余。以 `setTimeout` 為例子，它本身接受的值為毫秒，但很多開發場景常以秒為單位，如果為了這個單位轉換還要一個寫變數，只是入不敷出。大多數不具備搜索性或是重用性的常數，輔以註解即可。

當然，規則本身還是適用於大多數的常數，例如類型常數，規則本身就非常適用。還是要依據所處的環境來判斷。

ps: 如果你相信程式本身就是註解，不是懶就是蠢。

### 使用變數去承接取值操作，借用變數名稱來對取值的內容做解釋。

🌟 🌟 🌟 🌟

👻 👻

對於調用鏈過於複雜的取值，建議用中間變數來承接。

在部分應用場景下: 簡單的值變換過程，並且使用變換後值的地方不超過兩處。相比還要另外引入一個變數進來，會傾向直接把變換式丟給使用的地方。

### 減少使用縮寫的名稱帶來的心智負擔。

🌟 🌟

👻 👻 👻

使用縮寫在閱讀上，一定會造成一定程度上的困難。但閱讀程式不是做逐字解析。想要在每個小地方看出每個變數的含義，不如只抓大範圍的指代內容，和中間的變換過程。這條規則再加上`同類型意義的變數使用相同名稱`的規則，在開發上很容易讓變數的名稱最終只能走上越來越長的趨勢，造成另一種閱讀上，和開發上的困難。

一定程度上使用縮寫，可以有效的減少沒有太大意義的變數佔用名字的問題。

### 對複雜的結構，避免使用不必要的描述

🌟 🌟 🌟 🌟 🌟

👻

以物件為例，如果物件本身的名稱上就有對這包東西的描述，同樣的描述不應該在出現在內部的值名稱上。

### 在函式中使用預設參數，而非函式內部手動給予值。

🌟 🌟 🌟 🌟

👻

函式的參數給予預設參數，不僅可以設定預設值，還能在一定程度上作為簡易的文檔。

要注意的是，這邊只有處理 `undefined` 的情況，所以值的檢查還是不能少。

## 函式

### 函式的參數不能太多，少於兩個為佳

🌟 🌟 🌟 🌟 🌟

👻 👻 👻 👻 👻

函式的參數減少，最直接帶來的不是函式承載的功能複雜度下降，而是設計重用函式工具時，不會有所受限。按照順序傳遞參數調用函式，容易在函式功能發生變動造成參數增加時，難以兼容前面的寫法，最終導致參數的順序設計毫無邏輯可言。增加一點調用函式的複雜度，可以帶來函式工具組在參數的部分大幅度的解放。


### 函式的功能要遵行原子性

🌟 🌟

👻 👻 👻 👻 👻

不應該承載太多功能在單一的函式身上，但真的要做到原子性的程度倒也不用。由於開發實務上的多樣性，原子性只要能體現在功能面即可，程式面的部分，由於需要做第三方功能的封裝，外部值的變換封裝等內容，相比程式面上的原子性，功能面上的原子性更能提升可讀性。

### 函式名稱應體現其實際做的行為

🌟 🌟 🌟 🌟 🌟

👻 👻

### 函式只做一層抽象

### 刪除重複的程式

🌟 🌟 🌟 🌟 🌟

👻 👻 👻

有兩個以上重複的就應該重新設計，以便後續在更改響相應邏輯時，可以在一處完成即可。

### 不要使用狀態標誌作為參數

🌟

👻 👻

這部分主要是為了因應 `函式功能遵循原子性` 的規則。但由於個人見解功能面上的原子性更為重要，將狀態標誌作為參數並不影響功能面的原子性問題。

### 避免副作用

🌟 🌟 🌟 🌟 🌟

👻 👻 👻 👻 👻

如果能避免函式的副作用，在函式的組合上更為方便。`js`在開發上不能完全避免副作用，但應該將副作用限定在某一個小區域內。

### 不寫全域函式

🌟 🌟 🌟 🌟 🌟

👻 👻 👻

寫全域能避免類似循環調用（但不保證執行結果），調用方便，黑魔法等。但還是需要盡量避免做這類操作。慎選。

### 使用 FP 代替 IP

🌟 🌟 🌟 🌟 🌟

👻 👻 👻 👻 👻

FP就是好。

### 應該用函式封裝狀態相關邏輯

🌟 🌟 🌟

👻 👻

見仁見智，但有超過兩處地方需要使用時，就應該抽出成函式處理。

### 避免負面狀態（避免 ! 的使用）

🌟 🌟

👻

函式流程設計的問題。如果為了函式功能流程上的需要，還是會選擇 `!` 的使用。遵循的原則在上面提過，閱讀程式更注重中間的流程，而非單一的值或狀態的內容。

### 避免使用條件式

🌟

👻

比起程式面上的原子性，功能面上的原子性更重要。拋棄使用條件式，並不能對功能面上的原子性有太大的幫助。

### 避免型別（Type）檢查

🌟

👻

`避免使用條件式`的擴充規則。重複的不再贅述，但類型檢查完全不可避免。以第三方資料來說，你不能預期第三方資料來的格式會如何，若不做型別檢查，只會讓結果有更多問題。要做型別檢查也不一定要直接套上類似`typescript`的靜態類型檢查，先不說它本身使用後會帶來新的問題，以程式的邏輯面來說，你不提供你對預期變數類型的檢查，函式的功能本身就是不完全的。

### 不要過度優化

🌟 🌟 🌟

👻

### 移除沒有用處的程式

🌟 🌟

👻 👻 👻

雖然現在的程式都已經納入了版控，但面對無人管理的 `commit` 和頻繁修改的需求，將暫時無用的程式註解或留在專案裡，才是相對合理的選擇。或許會刪除，但也要等到穩定版之後的事了。




