# -ERP-HM-
ERPHM
這是一個非常實用、簡潔的 **ERP 表格處理系統前端範例**，它可以即時輸入品項、價格與數量，自動計算每列的金額，並支援新增與刪除列的功能。👍

以下是我對這段程式碼的簡要優化建議與擴充建議：

---

### ✅ 現有功能概述：

* 可新增商品列（品名、單價、數量）
* 即時計算「單價 × 數量」的總金額
* 可移除某列商品
* 使用 jQuery 操作 DOM，邏輯清晰

---

### ✅ 建議加強功能（你可以選擇加進去）：

#### 1. **總合金額顯示**

加入一個 `<div id="grandTotal">`，顯示所有列的合計金額：

```html
<h3>總計金額：<span id="grandTotal">0</span> 元</h3>
```

並在 JavaScript 中加入自動統計：

```js
function updateGrandTotal() {
  let grandTotal = 0;
  $('#erpTable .total').each(function () {
    grandTotal += parseFloat($(this).text()) || 0;
  });
  $('#grandTotal').text(grandTotal.toFixed(2));
}

// 在更新單筆金額時，順便更新總計
$('#erpTable').on('input', '.price, .qty', function () {
  const row = $(this).closest('tr');
  const price = parseFloat(row.find('.price').val()) || 0;
  const qty = parseFloat(row.find('.qty').val()) || 0;
  const total = price * qty;
  row.find('.total').text(total.toFixed(2));
  updateGrandTotal(); // 更新總金額
});

// 在刪除列時更新總金額
$('#erpTable').on('click', '.remove', function () {
  $(this).closest('tr').remove();
  updateGrandTotal(); // 更新總金額
});
```

---

#### 2. **資料驗證提示（可選）**

讓欄位輸入錯誤時顯示警告，例如數量不能為負數、單價不能為 0。

---

#### 3. **加入儲存 / 匯出功能（可選）**

可以將表格匯出成 JSON 或 CSV 檔案（若你有需要我可以幫你加上）。

---

#### 4. **多語系支援（可選）**

你未來若要英文介面，只要將 `<th>` 與文字部分抽出來即可支援切換。

---

是否需要我幫你整合以上優化（特別是 **總計功能與儲存按鈕**）？還是你要我幫你升級成有後端（例如 Flask 或 Node.js）的版本？

