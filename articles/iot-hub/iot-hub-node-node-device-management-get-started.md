---
title: "開始使用裝置管理 | Microsoft 文件"
description: "本教學課程說明如何在 Azure IoT 中樞上開始使用裝置管理"
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: e044006d-ffd6-469b-bc63-c182ad066e31
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
translationtype: Human Translation
ms.sourcegitcommit: c18a1b16cb561edabd69f17ecebedf686732ac34
ms.openlocfilehash: 829164eaa856d824ed1f37c43799dabb8f0a0868


---
# <a name="tutorial-get-started-with-device-management"></a>教學課程：開始使用裝置管理
## <a name="introduction"></a>簡介
IoT 雲端應用程式可以使用 Azure IoT 中樞中的基本項目 (也就是裝置對應項和直接方法) 來遠端啟動並監視裝置上的裝置管理動作。  本文提供 IoT 雲端應用程式和裝置如何共同運作，以使用 IoT 中樞初始化並監視遠端裝置重新啟動的指導方針和程式碼。

若要從雲端式的後端 App 遠端啟動並監視您裝置上的裝置管理行動，請使用[裝置對應項][lnk-devtwin]和[直接方法][lnk-c2dmethod]等 Azure IoT 中樞基本類型。 本教學課程會示範後端 App 和裝置如何共同運作，以讓您從 IoT 中樞初始化並監視遠端裝置重新啟動。

您可以使用直接方法從雲端中的後端應用程式起始裝置管理動作 (例如重新啟動、恢復出廠預設值，以及韌體更新)。 該裝置將負責：

* 處理從 IoT 中樞傳送的方法要求。
* 在裝置上初始化相對應的裝置特定動作。
* 透過針對 IoT 中樞的報告屬性提供狀態更新。

您可以在雲端中使用後端 App 來執行裝置對應項查詢，以報告裝置管理動作的進度。

本教學課程說明如何：

* 使用 Azure 入口網站來建立 IoT 中樞，並且在 IoT 中樞建立裝置識別。
* 建立模擬的裝置應用程式，其具有可以由雲端呼叫以進行重新啟動的直接方法。
* 建立主控台應用程式，可透過您的 IoT 中樞在模擬的裝置應用程式中呼叫重新啟動直接方法。

在本教學課程結尾處，您會有兩個 Node.js 主控台應用程式：

**dmpatterns_getstarted_device.js**，它會以先前建立的裝置識別連線到您的 IoT 中樞，接收重新啟動直接方法，模擬實體重新啟動，並報告上一次重新啟動的時間。

**dmpatterns_getstarted_service.js**，它會在模擬裝置應用程式上呼叫直接方法，顯示回應，並顯示更新的報告屬性。

若要完成此教學課程，您需要下列項目：

* Node.js 0.12.x 版或更新版本， <br/>  [準備您的開發環境][lnk-dev-setup]說明如何在 Windows 或 Linux 上安裝本教學課程的 Node.js。
* 使用中的 Azure 帳戶。 (如果您沒有帳戶，只需要幾分鐘的時間就可以建立[免費帳戶][lnk-free-trial]。)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>建立模擬裝置應用程式
在本節中，您將：

* 建立 Node.js 主控台應用程式，以回應雲端所呼叫的直接方法
* 觸發模擬裝置重新啟動
* 使用報告屬性來啟用裝置對應項查詢，以識別裝置及其上次重新啟動時間

1. 建立稱為 **manageddevice**的新的空資料夾。  在 **manageddevice** 資料夾中，於命令提示字元使用下列命令建立 package.json 檔案。  接受所有預設值：
   
    ```
    npm init
    ```
2. 在命令提示字元中，於 **manageddevice** 資料夾中執行下列命令來安裝 **azure-iot-device** 裝置 SDK 套件和 **azure-iot-device-mqtt** 套件：
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. 使用文字編輯器，在 [manageddevice] 資料夾中建立新的 **dmpatterns_getstarted_device.js** 檔案。
4. 在 **dmpatterns_getstarted_device.js** 檔案開頭新增下列 'require' 陳述式：
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. 新增 **connectionString** 變數，並用它來建立裝置用戶端。  以您裝置的連接字串取代連接字串。  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. 新增下列函式以在裝置上實作直接方法
   
    ```
    var onReboot = function(request, response) {
   
        // Respond the cloud app for the direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report the reboot before the physical restart
        var date = new Date();
        var patch = {
            iothubDM : {
                reboot : {
                    lastReboot : date.toISOString(),
                }
            }
        };
   
        // Get device Twin
        client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                console.log('twin acquired');
                twin.properties.reported.update(patch, function(err) {
                    if (err) throw err;
                    console.log('Device reboot twin state reported')
                });  
            }
        });
   
        // Add your device's reboot API for physical restart.
        console.log('Rebooting!');
    };
    ```
7. 開啟您 IoT 中樞的連線，並啟動直接方法接聽程式︰
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not open IotHub client');
        }  else {
            console.log('Client opened.  Waiting for reboot method.');
            client.onDeviceMethod('reboot', onReboot);
        }
    });
    ```
8. 儲存並關閉 **dmpatterns_getstarted_device.js**檔案。
   
   [AZURE.NOTE] 為了簡單起見，本教學課程不會實作任何重試原則。 在實際程式碼中，您應該如 MSDN 文章[暫時性錯誤處理][lnk-transient-faults]所建議，實作重試原則 (例如指數型輪詢)。

## <a name="trigger-a-remote-reboot-on-the-device-using-a-direct-method"></a>使用直接方法在裝置上觸發遠端重新啟動
在本節中，您會建立一個 Node.js 主控台 App，此 App 會使用直接方法在裝置上初始化遠端重新啟動，並使用裝置對應項 (twin) 查詢來尋找該裝置的上次重新啟動時間。

1. 建立名為 **triggerrebootondevice** 的新空白資料夾。  在命令提示字元中，於 [triggerrebootondevice] 資料夾中使用下列命令來建立 package.json 檔案。  接受所有預設值：
   
    ```
    npm init
    ```
2. 在 **triggerrebootondevice** 資料夾中，於命令提示字元執行下列命令以安裝 **azure-iothub** 裝置 SDK 套件以及 **azure-iot-device-mqtt** 套件：
   
    ```
    npm install azure-iothub --save
    ```
3. 使用文字編輯器，在 [triggerrebootondevice] 資料夾中建立新的 **dmpatterns_getstarted_service.js** 檔案。
4. 在 **dmpatterns_getstarted_service.js** 檔案開頭新增下列 'require' 陳述式：
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. 新增下列變數宣告，並取代預留位置值︰
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToReboot = 'myDeviceId';
    ```
6. 新增下列函式來叫用裝置方法，以重新啟動目標裝置︰
   
    ```
    var startRebootDevice = function(twin) {
   
        var methodName = "reboot";
   
        var methodParams = {
            methodName: methodName,
            payload: null,
            timeoutInSeconds: 30
        };
   
        client.invokeDeviceMethod(deviceToReboot, methodParams, function(err, result) {
            if (err) { 
                console.error("Direct method error: "+err.message);
            } else {
                console.log("Successfully invoked the device to reboot.");  
            }
        });
    };
    ```
7. 新增下列函式來查詢裝置並取得上次重新啟動時間︰
   
    ```
    var queryTwinLastReboot = function() {
   
        registry.getTwin(deviceToReboot, function(err, twin){
   
            if (twin.properties.reported.iothubDM != null)
            {
                if (err) {
                    console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
                } else {
                    var lastRebootTime = twin.properties.reported.iothubDM.reboot.lastReboot;
                    console.log('Last reboot time: ' + JSON.stringify(lastRebootTime, null, 2));
                }
            } else 
                console.log('Waiting for device to report last reboot time.');
        });
    };
    ```
8. 新增下列函式來呼叫將觸發重新啟動直接方法並查詢上次重新啟動時間的函式︰
   
    ```
    startRebootDevice();
    setInterval(queryTwinLastReboot, 2000);
    ```
9. 儲存並關閉 **dmpatterns_getstarted_service.js** 檔案。

## <a name="run-the-apps"></a>執行應用程式
您現在可以開始執行應用程式。

1. 在 **manageddevice** 資料夾中，於命令提示字元中執行下列命令以開始接聽重新啟動直接方法。
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. 在命令提示字元中，於 [triggerrebootondevice] 資料夾中執行下列命令來觸發遠端重新啟動，以及查詢裝置對應項 (twin) 來尋找上次重新啟動時間。
   
    ```
    node dmpatterns_getstarted_service.js
    ```
3. 您會在主控台中看到直接方法的裝置回應。

## <a name="customize-and-extend-the-device-management-actions"></a>自訂及延伸裝置管理動作
您的 IoT 解決方案可以透過使用裝置對應項 (twin) 和直接方法基本類型，擴充一組已定義的裝置管理模式或啟用自訂模式。 其他裝置管理動作範例還包括恢復出廠預設值、韌體更新、軟體更新、電源管理、網路和連線管理，以及資料加密。

## <a name="device-maintenance-windows"></a>裝置維護期間
一般而言，您會設定讓裝置在產生最短中斷和停機時間的時機執行動作。  裝置維護期間是用來定義裝置組態更新時機的常用模式。 您的後端解決方案可以使用所需的裝置對應項 (twin) 屬性，在您的裝置上定義可啟用維護期間的原則並啟用該原則。 當裝置收到維護期間原則時，它可以使用回報的裝置對應項 (twin) 屬性來回報原則的狀態。 接著，後端 App 便可使用裝置對應項 (twin) 查詢來證明是否符合裝置及每個原則的規定。

## <a name="next-steps"></a>後續步驟
在本教學課程中，您已使用直接方法來觸發裝置上的遠端重新啟動、使用報告屬性來從裝置回報上次重新啟動時間，以及查詢裝置對應項來從雲端探索裝置的上次重新啟動時間。

若要繼續開始使用「IoT 中樞」和裝置管理模式 (例如遠端無線韌體更新)，請參閱︰

[教學課程：如何進行韌體更新][lnk-fwupdate]

若要了解如何擴充您的 IoT 解決方案以及在多個裝置上排程方法呼叫，請參閱[排程及廣播作業][lnk-tutorial-jobs]教學課程。

若要繼續開始使用 IoT 中樞，請參閱[開始使用 IoT 閘道 SDK][lnk-gateway-SDK]。

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdks/blob/master/doc/get_started/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[Azure portal]: https://portal.azure.com/
[Using resource groups to manage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-gateway-SDK]: iot-hub-linux-gateway-sdk-get-started.md

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx



<!--HONumber=Nov16_HO5-->


