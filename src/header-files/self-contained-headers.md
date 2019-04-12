## 自給自足標頭檔 (Self-contained Headers)

> 標頭檔應該要自給自足 (self-contained)，而且副檔名必須是 `.h`。 其他具有插入目的，但不是標頭檔者，則應該要使用 `.inc` 作為副檔名，並且應該盡少使用。

所有標頭檔都應該要自給自足。 換句話說，使用者或者重構工具 (Refractoring Tool) 並不需要依賴任何額外的條件才能夠插入標頭檔。 更精確地說，標頭檔應該要包含 [標頭檔保護](define-guard.md)，而且應該要自己插入所有需要的其他標頭檔。

建議將模板與行內函式的定義放在同樣的檔案作為宣告。 所有使用到這些東西的 `.cc` 檔都應該要載入這些結構，不然在某些建置設定下會造成程式無法連結。 如果將定義與宣告分別在不同檔案，載入宣告的話也應該要能夠同時載入其定義。 不要將這些定義移至額外的 `-inl.h` 檔中。 這種作法在過去很常見，但是從現在開始不允許這麼做。

有一個例外是，函式模板的顯式實體化 (explicitly instantiated) 或者該模板是一個類別的私有成員的話，可以只定義在實體化該模板的 `.cc` 檔中。

在某些極少數的狀況下，標頭檔可以不用是自給自足的。 這些特殊的標頭檔通常是用來載入程式碼到做一些不尋常的位置，例如載入到另一個檔案的中間。 他們可以不使用 [標頭檔保護](define-guard.md)，而且可能沒有載入他們所需的檔案。 這種類型的檔案應該使用 `.inc` 作為副檔名。 盡量別使用這種檔案，可能的話還是盡量用自給自足的標頭檔。