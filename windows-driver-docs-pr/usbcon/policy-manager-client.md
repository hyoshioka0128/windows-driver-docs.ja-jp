---
Description: クライアントドライバーは、USB タイプ C コネクタのポリシーの決定に参加できます。
title: USB Type-C ポリシー マネージャー クライアント ドライバーを記述する
ms.date: 10/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: b4eda3a32eba49b8fc35bfbc834fd9f246bee495
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824242"
---
# <a name="write-a-usb-type-c-policy-manager-client-driver"></a>USB Type-C ポリシー マネージャー クライアント ドライバーを記述する

Microsoft 提供の USB タイプ C ポリシーマネージャーは、USB タイプ C コネクタのアクティビティを監視します。 Windows version 1809 では、クライアントドライバーをポリシーマネージャーに書き込むために使用できる一連のプログラミングインターフェイスが導入されています (このトピックでは、 _PM クライアントドライバー_と呼ばれています)。 クライアントドライバーは、USB タイプ C コネクタのポリシーの決定に参加できます。 このセットを使用して、カーネルモードのエクスポートドライバーまたはユーザーモードドライバーを作成できます。

ポリシーマネージャーは、USB コネクタマネージャー (UCM)、USB ホストコントローラー、USB 機能、および PM クライアントドライバーから情報を取得し、調整します。 UI 通知が必要な場合は、ポリシーマネージャーが要求をシステムシェルに送信します。

![USB ポリシーマネージャーの Architechtural ブロック図](images/pmclient.png)

ドライバーの詳細については、「[アーキテクチャ: Windows システム用の USB タイプ C の設計](https://docs.microsoft.com/windows-hardware/drivers/usbcon/architecture--usb-type-c-in-a-windows-system)」を参照してください。

## <a name="important-apis"></a>重要な API
PM Api は、 [Usbpmapi .h](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbpmapi)ヘッダーで宣言されています。
 
## <a name="1-client-registration"></a>1: クライアント登録

1. クライアントドライバーは[**UsbPm_Register**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbpmapi/nf-usbpmapi-usbpm_register)を呼び出して、ドライバーのコールバック関数を登録します。
2. クライアントドライバーは、ポリシーマネージャーからのイベントを待機します。 
    > 正常に**UsbPm_Register**を呼び出すと、クライアントドライバーがアクセスを要求したことは保証されません。 ポリシーマネージャーの準備が整うと、実際に付与されたアクセス権を示すイベントデータとして、 **Policymanagerarrival**でドライバーの[**EVT_USBPM_EVENT_CALLBACK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbpmapi/nc-usbpmapi-evt_usbpm_event_callback)が呼び出されます。
3. **UsbPm_Register**の呼び出しでは、登録ハンドルが返されます。
    > クライアントドライバーは、 **UsbPm_Register**が戻る前でも、 **EVT_USBPM_EVENT_CALLBACK**を受け取ることがあります。

## <a name="2-hub-arrival"></a>2: ハブへの到着

1. UCMCX デバイスが到着すると、ポリシーマネージャーに通知され、各ハブのすべてのコネクタのプロパティと状態と共に、すべてのハブハンドルが記録されます。
2. クライアントドライバーの[**EVT_USBPM_EVENT_CALLBACK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbpmapi/nc-usbpmapi-evt_usbpm_event_callback)は、イベントデータとして**HubArrivalRemoval**を使用して呼び出されます。 この呼び出しには、ハブハンドルも含まれています。
3. クライアントドライバーの**EVT_USBPM_EVENT_CALLBACK**の実装では、ドライバーは[**UsbPm_RetrieveHubProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbpmapi/nf-usbpmapi-usbpm_retrievehubproperties)を呼び出してハブ上のコネクタの数を取得し、 [**UsbPm_RetrieveConnectorProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbpmapi/nf-usbpmapi-usbpm_retrieveconnectorproperties)と UsbPm_ を呼び出します。 [**RetrieveConnectorState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbpmapi/nf-usbpmapi-usbpm_retrieveconnectorstate)を参照して、各コネクタに関する詳細情報を取得します。

## <a name="3-connector-state-change"></a>3: コネクタの状態の変更 
1. コネクタの状態が変更された (たとえば、タイプ C のアタッチ/デタッチ、PD コントラクトのネゴシエートなど) ため、ポリシーマネージャーはコネクタごとの状態情報を更新します。 
2. クライアントドライバーの[**EVT_USBPM_EVENT_CALLBACK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbpmapi/nc-usbpmapi-evt_usbpm_event_callback)は、イベントデータとして**ConnectorStateChange**を使用して呼び出されます。 この呼び出しには、コネクタハンドルも含まれています。
3. クライアントドライバーの完了ルーチンも呼び出され、それに応じてアクションを実行します。
4. クライアントドライバーの**EVT_USBPM_EVENT_CALLBACK**の実装では、ドライバーは[**UsbPm_RetrieveConnectorProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbpmapi/nf-usbpmapi-usbpm_retrieveconnectorproperties)を呼び出します。 指定されたコネクタを使用して、driverto 最新のコネクタ状態を取得するように処理することで、ドライバーを検査し、ローカルコピーを更新することができます。  
 
## <a name="4-change-initiated-by-the-client-driver"></a>4: クライアントドライバーによって開始された変更

1. 変更を要求するために、クライアントドライバーは[**UsbPm_AssignConnectorPowerLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbpmapi/nf-usbpmapi-usbpm_assignconnectorpowerlevel)を呼び出します。
    > クライアントドライバーは、 **UsbPm_Register**を使用して登録された**EVT_USBPM_EVENT_CALLBACK**コールバック内でこの関数を呼び出すことができます。

2. ポリシーマネージャーは、要求を USB コネクタマネージャー (UCM) に転送します。 UcmCx のクライアントドライバーは、要求された状態を変更するための適切なアクションを実行します。
3. クライアントドライバーの[**EVT_USBPM_EVENT_CALLBACK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbpmapi/nc-usbpmapi-evt_usbpm_event_callback)は、イベントデータとして**ConnectorStateChange**を使用して呼び出されます。 この呼び出しには、コネクタハンドルも含まれています。
4. クライアントドライバーの完了ルーチンも呼び出され、それに応じてアクションを実行します。
5. コールバック内で、クライアントドライバーは、指定されたコネクタハンドルを使用して[**UsbPm_RetrieveConnectorState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbpmapi/nf-usbpmapi-usbpm_retrieveconnectorproperties)を呼び出し、コネクタの最新の状態を取得し、それを検査して、ローカルコピーを更新することを決定します。

 
## <a name="5-hub-removal"></a>5: ハブの削除

1. UCM は、ucmcx デバイスの個別のコネクタではなく UcmCx デバイスが削除された場合に、ポリシーマネージャーに通知します。 ポリシーマネージャーはハブコレクションからハブを削除します。
2. クライアントドライバーの[**EVT_USBPM_EVENT_CALLBACK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbpmapi/nc-usbpmapi-evt_usbpm_event_callback)実装は、 **HubRemoval**を使用してイベントデータとして呼び出されます。 この呼び出しには、ハブハンドルも含まれています。
3. クライアントドライバーの**EVT_USBPM_EVENT_CALLBACK**の実装では、クライアントドライバーは、削除されるハブとコネクタに対してクリーンアップタスクを実行します。 ドライバーは[**UsbPm_RetrieveHubProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbpmapi/nf-usbpmapi-usbpm_retrievehubproperties)と[**UsbPm_RetrieveConnectorProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbpmapi/nf-usbpmapi-usbpm_retrieveconnectorproperties)を呼び出して、ハブとコネクタのプロパティを取得できます。
 
## <a name="6-client-deregistration"></a>6: クライアントの登録解除 
1. クライアントドライバーは、ドライバーが通知を必要としなくなったときに[**UsbPm_Deregister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbpmapi/nf-usbpmapi-usbpm_register)を呼び出します。
2. ポリシーマネージャーは、クライアントハンドル登録を登録解除としてマークし、 **EVT_USBPM_EVENT_CALLBACK**コールバックを呼び出しません。

## <a name="see-also"></a>参照

[USB タイプの C コネクタドライバーを作成する](https://docs.microsoft.com/windows-hardware/drivers/usbcon/bring-up-a-usb-type-c-connector-on-a-windows-system)

[USB タイプの C ポートコントローラードライバーを作成する](https://docs.microsoft.com/windows-hardware/drivers/usbcon/write-a-usb-type-c-port-controller-driver)

[USB 関数コントローラークライアントドライバーを作成する](https://docs.microsoft.com/windows-hardware/drivers/usbcon/function-client-driver)
