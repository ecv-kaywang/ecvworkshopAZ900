#  ECV AZ900 Workshop 


### 登入 Azure Portal
在 https://portal.azure.com 登入 Azure 入口網站。

## Lab 1 : 在虛擬機器上新增 IIS 
#### 學習目標：
* 建立 Windows 虛擬機
* 透過 Powershell 安裝 IIS 
* 設置安全的 RDP

#### 架構圖：
![](https://i.imgur.com/9T0aPy3.jpg)

### 新增 一台 windows 虛擬機器
* 在搜尋列搜尋`虛擬機器`
* 出現後點選虛擬機器

![](https://i.imgur.com/NJZfVPO.png)

* 點選**建立**，選擇 Azure虛擬機器

![](https://i.imgur.com/QwpmOtg.png)

* [基本] 索引標籤中，輸入下列資訊：
	* 資源群組：按下新增，命名`my-az900-test`
	* 虛擬機器名稱: 請自行命名，例如：`win2019-test-vm`
	* 區域: 可選用`(US) East US 2`

![](https://i.imgur.com/2pbrmL9.png)

* 其他設定
	* 點選所有影像，找到`Windows Server 2019 Datacenter - Gen 2`
	* 大小：可選擇 `Standard_D4ds_v5`
	* 帳號：`azureuser`
	* 密碼：`z9J5:O*jqx)y`
	* 公用輸入連接埠：選擇 80 與 3389

![](https://i.imgur.com/q9z00fV.png)

* 輸入好後，按**下一步：磁碟**

* [磁碟] 索引標籤中，輸入下列資訊：
	* 選擇: 標準 SSD
	* 接著：按**下一步：網路**
![](https://i.imgur.com/iWRNtU9.png)
* 網路
	* 勾選: 刪除 VM 時刪除公用 IP 和 NIC
	* 按**下一步：管理**

![](https://i.imgur.com/vH7iGlL.png)

* [管理]索引標籤中，輸入下列資訊：
	* 可設定自動關機
	
![](https://i.imgur.com/T8J0pfS.png)
* 	點選**檢閱＋建立**
* 	驗證成功後，按下**建立**
![](https://i.imgur.com/ud03E8g.png)

* 按下**前往資源**

![](https://i.imgur.com/l4sAwNA.png)

### 透過 Powershell 安裝 IIS
* 	找到左側選單 作業 > 執行命令 > RunPowerShellScript

![](https://i.imgur.com/TpPooaH.png)

* 複製貼上以下指令
```
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```
![](https://i.imgur.com/ElUgYWS.png)

* 等待幾分鐘後，輸出畫面出現成功訊息

![](https://i.imgur.com/F772Mqc.png)


* 到**概觀** > **複製公用 IP 位址**


![](https://i.imgur.com/UZ5yGVb.png)

* 打開瀏覽器，數入剛剛複製的公用 IP 位址，就可以看到以下畫面

![](https://i.imgur.com/rcpsb9a.png)

### 設置安全的 RDP
* 在**網路** > 在輸入連接埠規則點選 **RDP**

![](https://i.imgur.com/hqbQhNq.png)

* 來源改成 **IP Addresses**
* 在來源 IP 位址輸入你的公司的聯網 IP 或是輸入目前的IP
	* 找到目前的IP
	https://www.myip.com/


![](https://i.imgur.com/YbEN4BH.png)


* 按下存儲成功後

![](https://i.imgur.com/cNRyZWD.png)


* 到 **連線**，**下載 RDP 檔案**

![](https://i.imgur.com/YSHOFkH.png)

* 檢查連線
	

![](https://i.imgur.com/ITf89Wy.png)

* 透過介面檢查 ssh port 是否開啟

![](https://i.imgur.com/b2n0xN1.png)

* 開機診斷
	* 透過序列紀錄檔查看開機狀態

![](https://i.imgur.com/fzuFHTs.png)





## Lab 2 : 透過 Azure Storage 建立靜態網站
#### 學習目標 :
* 建立 Azure Storage account
* 啟用 Azure Cloud Shell
* 透過 git 下載 index.html
* 在 Azure Storage Account 啟用靜態網站

#### 架構圖：
![](https://i.imgur.com/QuaaGay.jpg)

### 新增 Azure Storage account
* 搜尋`儲存體帳戶`

![](https://i.imgur.com/PtCZufo.png)

* 按下**建立**
![](https://i.imgur.com/L13pfcC.png)

* [基本] 索引標籤中，輸入下列資訊：
	* 資源群組：選擇`my-az900-test`
	* 儲存體帳戶名稱：虛要是唯一值請自行命名，例如：<your name + today date>
	* 區域：選擇離你最近的區域
	* 效能：標準
	* 備援：本機備援儲存體 (LRS)

![](https://i.imgur.com/bSiX2uj.png)

* 按**下一步：進階**
* [進階] 索引標籤中，輸入下列資訊：
	* 存取層：經常性
	
![](https://i.imgur.com/qnjgGJq.png)

* 按**下一步：網路**

![](https://i.imgur.com/D1r50S9.png)

* 點選**檢閱＋建立**
	* 確認內容後，點選建立

![](https://i.imgur.com/W5nzpDE.png)

* 部署完成後，點選**前往資源**


![](https://i.imgur.com/rF6YBmo.png)

###  啟用 Azure Cloud Shell
* 點選右上角圖示

![](https://i.imgur.com/IBnqo4m.png)

* 點選 **Bash**

![](https://i.imgur.com/vQKsAIF.png)

* 點選 **顯示進階設定**

![](https://i.imgur.com/hNGAfl9.png)

* 進階設定
	* 資源群組，點選使用現有項目，選擇剛剛建立的群組
	* 儲存體帳戶，點選使用現有項目，選擇剛剛建立的帳戶
	* 檔案共用，點選使用現有項目，**輸入**剛剛建立的帳戶
	* 接著，按下**連結儲存體**

![](https://i.imgur.com/PX0fxce.png)

### 透過 git 下載 index.html
* 在 Cloud Shell 命令提示字元下輸入：

```
git clone https://github.com/ecv-kaywang/ecvworkshopAZ900.git
```
![](https://i.imgur.com/QCtFd4K.png)

* 輸入以下指令
```
cd ecvworkshopAZ900/
code .
```
* 透過 Cloud Shell 編輯器右上角打開選單，關閉編輯器

![](https://i.imgur.com/x4Ag2nA.png)



* 點選左上角圖示，點選**下載**

![](https://i.imgur.com/nt2sHA6.png)


* 輸入檔案目錄與下載檔名：`/ecvworkshopAZ900/index.html`
* 點選**下載**

![](https://i.imgur.com/JQRs4kD.png)

* 點選右下角連結，下載檔案

![](https://i.imgur.com/XxYLmaa.png)

* 點選右上角 **X** ，關閉 Cloud Shell

#### 在 Azure Storage Account 啟用靜態網站
* 回到剛剛建好的 Azure Storage Account
	* 在左邊選單**資料管理**下方，點選**靜態網站**
	* 點選**已啟用**
	* 索引文件名稱，輸入：`index.html`
	* 記得**儲存**

![](https://i.imgur.com/pDkNSJc.png)

* 啟用成功後，點選系統建立的容器 **$web**

![](https://i.imgur.com/yNX0N4g.png)

* 上傳剛剛下載的 index.html

![](https://i.imgur.com/45JesVA.png)

* 上傳成功後，點選左上方**靜態網站**

![](https://i.imgur.com/j1I5yu0.png)

* 複製你的網站網址

![](https://i.imgur.com/1msFJ9S.png)

* 打開瀏覽器，將網址複製貼上
* 成功的話將看到下面這個頁面

![](https://i.imgur.com/NXwN9jm.png)



## 清除資源前，認識資源群組
* 點選首頁，回到資源群組
* 點選**活動紀錄**

![](https://i.imgur.com/HA6myA2.png)

* 點選**資源視覺化檢視**

![](https://i.imgur.com/6JC4c7G.png)

* 點選**部署**

![](https://i.imgur.com/laDeffz.png)

* 點選**成本分析**

![](https://i.imgur.com/jzSxXjq.png)

* 回到概觀，點選**刪除資源群組**

![](https://i.imgur.com/laNQNGX.png)

* **輸入資源群組名稱**，按下**刪除**

![](https://i.imgur.com/Tz7M1nf.png)





* 參考資料來源
> https://learn.microsoft.com/zh-tw/azure/virtual-machines/windows/quick-create-portal
> https://learn.microsoft.com/zh-tw/training/modules/describe-azure-storage-services/5-exercise-create-storage-blob
> https://learn.microsoft.com/zh-tw/azure/cloud-shell/features
> https://learn.microsoft.com/zh-tw/azure/storage/common/storage-introduction
> https://learn.microsoft.com/zh-tw/azure/cloud-shell/quickstart
