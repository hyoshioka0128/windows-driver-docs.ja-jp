---
title: デバイスインターフェイスの到着と削除の通知に登録する
description: このトピックでは、ユーザーモードのアプリケーションまたはドライバーがデバイスインターフェイスの到着とデバイスの削除に関する通知を登録する方法について説明します。
ms.assetid: 665E7881-F49C-4FC1-971C-1762B7D0C26E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7becd74e01b988f941195b180388d54589e91373
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837368"
---
# <a name="registering-for-notification-of-device-interface-arrival-and-device-removal"></a>デバイス インターフェイスの到着とデバイスの削除の通知の登録


このトピックでは、ユーザーモードのアプリケーションまたはドライバーがデバイスインターフェイスの到着とデバイスの削除に関する通知を登録する方法について説明します。

通常、ユーザーモードコンポーネントは、 [**CM_Register_Notification**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_register_notification)を呼び出してデバイスインターフェイスを検索し、そのインターフェイスに i/o 要求を送信します。 これを行うために、コンポーネントは**CM_NOTIFY_FILTER_TYPE_DEVICEINTERFACE**と**CM_NOTIFY_FILTER_TYPE_DEVICEHANDLE**の両方を登録します。これにより、デバイスインターフェイスの到着とデバイスの削除がそれぞれ通知されます。 呼び出しシーケンスは次のようになります。

**デバイス インターフェイスの到着とデバイスの削除の通知の登録**

1. **CM_NOTIFY_FILTER_TYPE_DEVICEINTERFACE**を使用して[**CM_Register_Notification**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_register_notification)を呼び出し、デバイスインターフェイスの到着通知を登録します。 指定したクラスの今後のインターフェイスが到着すると、システムによってコンポーネントに通知されます。
2. I/o を送信するインターフェイスがシステムに既に存在している可能性があるため、 [**CM_Get_Device_Interface_List**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_device_interface_lista)または[**SetupDiGetClassDevs**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw)を呼び出して既存のインターフェイスの一覧を取得します。
   **メモ** 手順 1. と手順 2. の間にインターフェイスが到着した場合、手順 1. の登録と手順 2. のインターフェイスの一覧から、インターフェイスが2回表示されます。

     

3. 目的のインターフェイスを見つけたら、 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)を呼び出して、デバイスのハンドルを開きます。
4. 手順 3. でデバイスハンドルが正常に作成されたら、 [**CM_Register_Notification**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_register_notification)をもう一度呼び出します。 今回は、 **CM_NOTIFY_FILTER_TYPE_DEVICEHANDLE**型の通知を登録し、通知を受信するハンドルとして新しいデバイスハンドルを提供します。 インターフェイスによって表されるデバイスがクエリの削除要求を受け取ると、システムによってコンポーネントに通知されます。

5. このテーブルは、デバイスハンドル通知コールバックを実装するときに使用します。

   <div class="mx-tableFixed">
   <table>
   <colgroup>
   <col width="50%" />
   <col width="50%" />
   </colgroup>
   <thead>
   <tr class="header">
   <th align="left">コールバックによって受信されるアクション値</th>
   <th align="left">コンポーネントの動作</th>
   </tr>
   </thead>
   <tbody>
   <tr class="odd">
   <td align="left"><strong>CM_NOTIFY_ACTION_DEVICEQUERYREMOVE</strong></td>
   <td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/handleapi/nf-handleapi-closehandle" data-raw-source="[CloseHandle](https://docs.microsoft.com/windows/desktop/api/handleapi/nf-handleapi-closehandle)">CloseHandle</a>を呼び出してデバイスハンドルを閉じます。 この操作を行わないと、開いているハンドルによって、このデバイスのクエリ削除が成功しません。</p></td>
   </tr>
   <tr class="even">
   <td align="left"><strong>CM_NOTIFY_ACTION_DEVICEQUERYREMOVEFAILED</strong></td>
   <td align="left"><p>クエリの削除に失敗したため、デバイスとそのインターフェイスは引き続き有効です。 引き続きインターフェイスに i/o を送信するには、その新しいハンドルを開きます。</p>
   <p>まず、 <a href="https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification" data-raw-source="[&lt;strong&gt;CM_Unregister_Notification&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)"><strong>CM_Unregister_Notification</strong></a>を呼び出して、古いハンドルの通知の登録を解除します。 登録を解除する通知ハンドルの通知コールバックから<strong>CM_Unregister_Notification</strong>を呼び出すことはできないため、遅延ルーチンからこれを行う必要があります。  詳細については、 <a href="https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification" data-raw-source="[&lt;strong&gt;CM_Unregister_Notification&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)"><strong>CM_Unregister_Notification</strong></a>の「<strong>解説</strong>」を参照してください。</p>
   <p>次に、遅延ルーチンで続行するか、通知コールバックに戻り、 <a href="https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea" data-raw-source="[&lt;strong&gt;CreateFile&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)"><strong>CreateFile</strong></a>を呼び出して新しいハンドルを作成します。 次に、新しい handle と<strong>CM_NOTIFY_FILTER_TYPE_DEVICEHANDLE</strong>を使用して<a href="https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_register_notification" data-raw-source="[&lt;strong&gt;CM_Register_Notification&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_register_notification)"><strong>CM_Register_Notification</strong></a>を呼び出します。</p>
   <p><strong>CM_NOTIFY_ACTION_DEVICEQUERYREMOVE</strong>通知が送信された後にクエリを削除しようとしているデバイスで通知を登録すると、 <strong>CM_NOTIFY_ACTION_DEVICEQUERYREMOVEFAILED</strong>が表示される場合があることに注意してください。通知は、最初に<strong>CM_NOTIFY_ACTION_DEVICEQUERYREMOVE</strong>通知を受信しません。</p></td>
   </tr>
   <tr class="odd">
   <td align="left"><strong>CM_NOTIFY_ACTION_DEVICEREMOVEPENDING</strong></td>
   <td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification" data-raw-source="[&lt;strong&gt;CM_Unregister_Notification&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)"><strong>CM_Unregister_Notification</strong></a>を呼び出して、ハンドルの通知の登録を解除します。 これは、遅延ルーチンから実行する必要があります。  詳細については、 <a href="https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification" data-raw-source="[&lt;strong&gt;CM_Unregister_Notification&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)"><strong>CM_Unregister_Notification</strong></a>の「<strong>解説</strong>」を参照してください。  デバイスへのハンドルを開いたままの場合は、 <a href="https://docs.microsoft.com/windows/desktop/api/handleapi/nf-handleapi-closehandle" data-raw-source="[&lt;strong&gt;CloseHandle&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/handleapi/nf-handleapi-closehandle)"><strong>CloseHandle</strong></a>を呼び出してデバイスハンドルを閉じます。</p></td>
   </tr>
   <tr class="even">
   <td align="left"><strong>CM_NOTIFY_ACTION_DEVICEREMOVECOMPLETE</strong></td>
   <td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification" data-raw-source="[&lt;strong&gt;CM_Unregister_Notification&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)"><strong>CM_Unregister_Notification</strong></a>を呼び出して、ハンドルの通知の登録を解除します。 これは、遅延ルーチンから実行する必要があります。  詳細については、 <a href="https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification" data-raw-source="[&lt;strong&gt;CM_Unregister_Notification&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)"><strong>CM_Unregister_Notification</strong></a>の「<strong>解説</strong>」を参照してください。  デバイスへのハンドルを開いたままの場合は、 <a href="https://docs.microsoft.com/windows/desktop/api/handleapi/nf-handleapi-closehandle" data-raw-source="[&lt;strong&gt;CloseHandle&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/handleapi/nf-handleapi-closehandle)"><strong>CloseHandle</strong></a>を呼び出してデバイスハンドルを閉じます。</p></td>
   </tr>
   </tbody>
   </table>
   </div>
     

6. デバイスの操作が完了したら、 [**CM_Unregister_Notification**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)を呼び出して、手順 1. で登録したインターフェイス通知コールバックの登録を解除します。

UMDF 2 ドライバーでこの手順に従う場合は、「コード例に[デバイスインターフェイスを使用](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-device-interfaces)する」を参照してください。 UMDF 2 ドライバーは、ドライバーの[*Evtdevicepreparehardware*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)コールバックルーチンで手順1-4 を実行し、ドライバーのデバイス削除コールバックルーチンの1つで手順 6. を実行する場合があります。

## <a name="related-topics"></a>関連トピック


[**CM_Register_Notification**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_register_notification)

[**CM_Unregister_Notification**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_unregister_notification)

[デバイス インターフェイスの使用](https://docs.microsoft.com/windows-hardware/drivers/wdf/using-device-interfaces)

 

 






