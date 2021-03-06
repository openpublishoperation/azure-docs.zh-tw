
本教學課程的最後階段是建立並執行新的應用程式。

1. 瀏覽至儲存壓縮專案檔案的位置，在電腦上將檔案解壓縮，然後在 Visual Studio 中開啟方案檔。
2. 按 **F5** 鍵，以重建專案並啟動應用程式。
3. 在應用程式的 **Insert a TodoItem** 中輸入有意義的文字，例如 *完成教學課程* ，然後按一下 [儲存]。
   
       如此會傳送 POST 要求到 Azure 中代管的新行動服務。要求中的資料會插入 TodoItem 資料表中。行動服務會傳回資料表中儲存的項目，並且在應用程式的第二個資料欄中顯示資料。
4. (選用) 在通用 Windows 解決方案中，將預設的開始專案變更為其他應用程式，並再次執行應用程式。
   
    請注意，從先前步驟中儲存的資料，會在應用程式啟動後從行動服務載入。
5. 回到 [Azure 傳統入口網站](https://manage.windowsazure.com/)，按一下 [資料] 索引標籤，然後按一下 [TodoItems] 資料表。
   
       如此可讓您瀏覽由應用程式插入資料表中的資料。
   
       ![](./media/mobile-services-javascript-backend-run-app/mobile-data-browse.png)

<!----HONumber=AcomDC_1203_2015-->