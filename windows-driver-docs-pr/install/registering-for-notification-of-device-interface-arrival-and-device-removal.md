---
title: デバイス インターフェイスの到着、削除の通知の登録
description: このトピックでは、デバイス インターフェイスの到着とデバイスの削除の通知用のユーザー モード アプリケーションまたはドライバーを登録する方法について説明します。
ms.assetid: 665E7881-F49C-4FC1-971C-1762B7D0C26E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a99928673cc2d9fa92228d0be366854b1dc2631c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387323"
---
# <a name="registering-for-notification-of-device-interface-arrival-and-device-removal"></a>デバイス インターフェイスの到着とデバイスの削除の通知の登録


このトピックでは、デバイス インターフェイスの到着とデバイスの削除の通知用のユーザー モード アプリケーションまたはドライバーを登録する方法について説明します。

通常、ユーザー モード コンポーネントを呼び出して[ **CM_Register_Notification** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_register_notification)デバイス インターフェイスと、インターフェイスへの送信 I/O 要求を検索します。 両方のためには、コンポーネントを登録します**CM_NOTIFY_FILTER_TYPE_DEVICEINTERFACE**と**CM_NOTIFY_FILTER_TYPE_DEVICEHANDLE**、デバイス インターフェイスの到着とデバイスの削除の通知それぞれします。 呼び出し元のシーケンスは、次のようになります。

**デバイス インターフェイスの到着とデバイスの削除の通知を登録します。**

1. 呼び出す[ **CM_Register_Notification** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_register_notification)で**CM_NOTIFY_FILTER_TYPE_DEVICEINTERFACE**デバイス インターフェイス着荷通知に登録します。 指定したクラスの将来のインターフェイスが到着したとき、システムは、コンポーネントを通知します。
2. 既に可能性が I/O を送信するインターフェイスを呼び出し、システム上に存在するため、 [ **CM_Get_Device_Interface_List** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_device_interface_lista)または[ **SetupDiGetClassDevs**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw)既存のインターフェイスの一覧を取得します。
   **注**手順 1. と手順 2. でインターフェイスのリストに登録から、2 回、手順 1. と手順 2 の間のインターフェイスが到着すると場合、インターフェイスを表示します。

     

3. 必要なインターフェイスを見つけたら、呼び出す[ **CreateFile** ](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)デバイスのハンドルを開く。
4. 手順 3. でデバイス ハンドルが正常に作成した後は[ **CM_Register_Notification** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_register_notification)を 2 回目です。 今回は、型の通知に登録**CM_NOTIFY_FILTER_TYPE_DEVICEHANDLE**、し、通知を受信する対象のハンドルとして、新しいデバイス ハンドルを指定します。 インターフェイスによって表されるデバイスが受信するクエリは、システム コンポーネントに通知要求を削除します。

5. デバイス ハンドルの通知コールバックを実装するときは、このテーブルを使用します。

   <div class="mx-tableFixed">
   <table>
   <colgroup>
   <col width="50%" />
   <col width="50%" />
   </colgroup>
   <thead>
   <tr class="header">
   <th align="left">アクションの値、コールバックを受け取る</th>
   <th align="left">どのようなコンポーネントが行う必要があります。</th>
   </tr>
   </thead>
   <tbody>
   <tr class="odd">
   <td align="left"><strong>CM_NOTIFY_ACTION_DEVICEQUERYREMOVE</strong></td>
   <td align="left"><p>呼び出す<a href="https://docs.microsoft.com/windows/desktop/api/handleapi/nf-handleapi-closehandle" data-raw-source="[CloseHandle](https://docs.microsoft.com/windows/desktop/api/handleapi/nf-handleapi-closehandle)">CloseHandle</a>デバイス ハンドルを閉じます。 これを行わない場合、開いているハンドルによって次の位置からこのデバイスのクエリの削除ができないようにします。</p></td>
   </tr>
   <tr class="even">
   <td align="left"><strong>CM_NOTIFY_ACTION_DEVICEQUERYREMOVEFAILED</strong></td>
   <td align="left"><p>デバイスとそのインターフェイスが現在も有効であるため、クエリの削除に失敗しました。 インターフェイスへの I/O の送信を続行するには、新しいハンドルを開きます。</p>
   <p>最初に、呼び出すことによって、古いハンドルのための通知の登録を解除<a href="https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification" data-raw-source="[&lt;strong&gt;CM_Unregister_Notification&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)"> <strong>CM_Unregister_Notification</strong></a>します。 呼び出すことができないため、遅延ルーチンから実行する必要があります<strong>CM_Unregister_Notification</strong>から通知のコールバックを登録解除は通知のハンドル。  参照してください、<strong>解説</strong>の<a href="https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification" data-raw-source="[&lt;strong&gt;CM_Unregister_Notification&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)"> <strong>CM_Unregister_Notification</strong> </a>詳細についてはします。</p>
   <p>次に、いずれか遅延のルーチンで、または続行、通知のコールバックの呼び出しに<a href="https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea" data-raw-source="[&lt;strong&gt;CreateFile&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)"> <strong>CreateFile</strong> </a>新しいハンドルを作成します。 呼び出して<a href="https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_register_notification" data-raw-source="[&lt;strong&gt;CM_Register_Notification&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_register_notification)"> <strong>CM_Register_Notification</strong> </a>新しいハンドルを持つと<strong>CM_NOTIFY_FILTER_TYPE_DEVICEHANDLE</strong>します。</p>
   <p>通知の処理中であるデバイスを登録する場合、クエリ削除した後、 <strong>CM_NOTIFY_ACTION_DEVICEQUERYREMOVE</strong>通知が送信されて、表示される、 <strong>CM_NOTIFY_ACTION_DEVICEQUERYREMOVEFAILED</strong>最初に通知を<strong>CM_NOTIFY_ACTION_DEVICEQUERYREMOVE</strong>通知します。</p></td>
   </tr>
   <tr class="odd">
   <td align="left"><strong>CM_NOTIFY_ACTION_DEVICEREMOVEPENDING</strong></td>
   <td align="left"><p>呼び出す<a href="https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification" data-raw-source="[&lt;strong&gt;CM_Unregister_Notification&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)"> <strong>CM_Unregister_Notification</strong> </a>ハンドルのための通知の登録を解除します。 これは、遅延ルーチンから行う必要があります。  参照してください、<strong>解説</strong>の<a href="https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification" data-raw-source="[&lt;strong&gt;CM_Unregister_Notification&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)"> <strong>CM_Unregister_Notification</strong> </a>詳細についてはします。  デバイスへの開いているハンドルがまだ場合呼び出す<a href="https://docs.microsoft.com/windows/desktop/api/handleapi/nf-handleapi-closehandle" data-raw-source="[&lt;strong&gt;CloseHandle&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/handleapi/nf-handleapi-closehandle)"> <strong>CloseHandle</strong> </a>デバイス ハンドルを閉じます。</p></td>
   </tr>
   <tr class="even">
   <td align="left"><strong>CM_NOTIFY_ACTION_DEVICEREMOVECOMPLETE</strong></td>
   <td align="left"><p>呼び出す<a href="https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification" data-raw-source="[&lt;strong&gt;CM_Unregister_Notification&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)"> <strong>CM_Unregister_Notification</strong> </a>ハンドルのための通知の登録を解除します。 これは、遅延ルーチンから行う必要があります。  参照してください、<strong>解説</strong>の<a href="https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification" data-raw-source="[&lt;strong&gt;CM_Unregister_Notification&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)"> <strong>CM_Unregister_Notification</strong> </a>詳細についてはします。  デバイスへの開いているハンドルがまだ場合呼び出す<a href="https://docs.microsoft.com/windows/desktop/api/handleapi/nf-handleapi-closehandle" data-raw-source="[&lt;strong&gt;CloseHandle&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/handleapi/nf-handleapi-closehandle)"> <strong>CloseHandle</strong> </a>デバイス ハンドルを閉じます。</p></td>
   </tr>
   </tbody>
   </table>
   </div>
     

6. デバイスが完了したら後で呼び出す[ **CM_Unregister_Notification** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)手順 1. で登録されているインターフェイス通知コールバックの登録を解除します。

2 の UMDF ドライバーでは、この手順に従っている場合は、次を参照してください。[を使用してデバイスのインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-device-interfaces)コード例についてはします。 2 の UMDF ドライバーはドライバーの手順 1 ~ 4 を実行する場合があります[ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバック ルーチン、および手順 6 での 1 つ、ドライバーのデバイスの削除コールバック ルーチン。

## <a name="related-topics"></a>関連トピック


[**CM_Register_Notification**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_register_notification)

[**CM_Unregister_Notification**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)

[デバイスのインターフェイスを使用します。](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-device-interfaces)

 

 






