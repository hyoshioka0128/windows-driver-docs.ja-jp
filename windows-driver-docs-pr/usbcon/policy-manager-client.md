---
Description: The client driver can participate in the policy decisions for USB Type-C connectors.
title: 型 C ポリシー マネージャーの USB クライアント ドライバーを作成します。
ms.date: 10/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: cd587e74ed4541f06974a0b4fda43f740315677b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560575"
---
# <a name="write-a-usb-type-c-policy-manager-client-driver"></a>型 C ポリシー マネージャーの USB クライアント ドライバーを作成します。

Microsoft から提供された USB 型 C ポリシー マネージャーは、USB 型-C# のコネクタのアクティビティを監視します。 Windows、バージョンは 1809、プログラミング ポリシー マネージャーにクライアント ドライバーを記述するのに使用できるインターフェイスのセットが導入されています (と呼ばれる、 _PM クライアント ドライバー_このトピックの「)。 クライアント ドライバーは、USB 型-C# のコネクタのポリシーの決定に参加できます。 この設定すると、エクスポート カーネル モード ドライバーまたはユーザー モード ドライバーを記述できます。

ポリシー マネージャーを取得し、USB コネクタ マネージャー (UCM)、USB ホスト コント ローラーと USB 関数、および、PM のクライアント ドライバーからの情報を調整します。 UI の通知が必要な場合は、ポリシー マネージャーは、システム シェルに要求を送信します。

![Architechtural ブロック図 USB Policy Manager](images/pmclient.png)

ドライバーの完全なビューは、次を参照してください。[アーキテクチャ。Windows システムの USB 型-C# のデザイン](https://docs.microsoft.com/windows-hardware/drivers/usbcon/architecture--usb-type-c-in-a-windows-system)します。

## <a name="important-apis"></a>重要な API
PM Api がで宣言されている、 [Usbpmapi.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi)ヘッダー。
 
## <a name="1-client-registration"></a>1:クライアントの登録

1. クライアント ドライバーの呼び出し[ **UsbPm_Register** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/nf-usbpmapi-usbpm_register)ドライバーのコールバック関数を登録します。
2. クライアント ドライバーは、ポリシー マネージャーからイベントを待機します。 
    > 正常に実行**UsbPm_Register**呼び出しが、クライアント ドライバーがアクセスを要求したことを保証していません。 Policy Manager 準備ができたら、ドライバーの[ **EVT_USBPM_EVENT_CALLBACK** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/nc-usbpmapi-evt_usbpm_event_callback)で呼び出される**PolicyManagerArrival**実績を示すイベント データとしてアクセスを許可します。
3. **UsbPm_Register**呼び出しは、登録ハンドルを返します。
    > クライアント ドライバーが表示される**EVT_USBPM_EVENT_CALLBACK**前であってもに、 **UsbPm_Register**を返します。

## <a name="2-hub-arrival"></a>2:ハブ到着

1. UCMCX デバイスが到着すると、ポリシー マネージャーに通知しの各ハブ上のすべてのコネクタのプロパティおよび状態と共にすべてのハブ ハンドルを追跡します。
2. クライアント ドライバーの[ **EVT_USBPM_EVENT_CALLBACK** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/nc-usbpmapi-evt_usbpm_event_callback)で呼び出される**HubArrivalRemoval**イベント データとして。 呼び出しには、ハブ ハンドルも含まれています。
3. クライアント ドライバーの実装で**EVT_USBPM_EVENT_CALLBACK**、ドライバー呼び出し[ **UsbPm_RetrieveHubProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/nf-usbpmapi-usbpm_retrievehubproperties)ハブで、コネクタの数を取得するには呼び出して、 [ **UsbPm_RetrieveConnectorProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/nf-usbpmapi-usbpm_retrieveconnectorproperties)と[ **UsbPm_RetrieveConnectorState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/nf-usbpmapi-usbpm_retrieveconnectorstate)詳細を取得するには各コネクタについて説明します。

## <a name="3-connector-state-change"></a>3:コネクタの状態の変更 
1. コネクタの状態が変更されたため、たとえば、型 C アタッチ/デタッチ、ネゴシエート、PD コントラクト ポリシー マネージャーは、コネクタの状態情報を更新します。 
2. クライアント ドライバーの[ **EVT_USBPM_EVENT_CALLBACK** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/nc-usbpmapi-evt_usbpm_event_callback)で呼び出される**ConnectorStateChange**イベント データとして。 呼び出しには、コネクタのハンドルも含まれています。
3. クライアント ドライバーの完了ルーチンは、呼び出され、それに応じてアクションを実行します。
4. クライアント ドライバーの実装で**EVT_USBPM_EVENT_CALLBACK**、ドライバー呼び出し[ **UsbPm_RetrieveConnectorProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/nf-usbpmapi-usbpm_retrieveconnectorproperties)します。 指定されたコネクタのハンドルを使用して、driverto はコネクタの最新の状態を取得、それを検査し、ローカル コピーを更新します。  
 
## <a name="4-change-initiated-by-the-client-driver"></a>4:クライアント ドライバーによって開始された変更

1. クライアント ドライバーの変更を要求する呼び出し[ **UsbPm_AssignConnectorPowerLevel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/nf-usbpmapi-usbpm_assignconnectorpowerlevel)します。
    > クライアント ドライバー内でこの関数を呼び出すことができます、 **EVT_USBPM_EVENT_CALLBACK**コールバックを使用して登録**UsbPm_Register**します。

2. ポリシー マネージャーは、USB コネクタ マネージャー (UCM) に、要求を転送します。 UcmCx 用のクライアント ドライバーでは、要求された状態を変更する適切なアクションを実行します。
3. クライアント ドライバーの[ **EVT_USBPM_EVENT_CALLBACK** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/nc-usbpmapi-evt_usbpm_event_callback)で呼び出される**ConnectorStateChange**イベント データとして。 呼び出しには、コネクタのハンドルも含まれています。
4. クライアント ドライバーの完了ルーチンは、呼び出され、それに応じてアクションを実行します。
5. クライアント ドライバーを呼び出し、コールバック内で[ **UsbPm_RetrieveConnectorState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/nf-usbpmapi-usbpm_retrieveconnectorproperties)コネクタの最新の状態を取得して、指定されたコネクタ ハンドルとそれを検査し、そのローカル コピーを更新することができます。

 
## <a name="5-hub-removal"></a>5:ハブの削除

1. UCM は、UcmCx デバイス (しない個々 のコネクタ UcmCx デバイス上) が削除されたポリシー マネージャーに通知します。 ポリシー マネージャーは、そのハブのコレクションからハブを削除します。
2. クライアント ドライバーの[ **EVT_USBPM_EVENT_CALLBACK** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/nc-usbpmapi-evt_usbpm_event_callback)と実装が呼び出される**HubRemoval**イベント データとして。 呼び出しには、ハブ ハンドルも含まれています。
3. クライアント ドライバーの実装で**EVT_USBPM_EVENT_CALLBACK**、クライアント ドライバーは、ハブと削除されるコネクタのクリーンアップ タスクを実行します。 ドライバーが呼び出せる[ **UsbPm_RetrieveHubProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/nf-usbpmapi-usbpm_retrievehubproperties)と[ **UsbPm_RetrieveConnectorProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/nf-usbpmapi-usbpm_retrieveconnectorproperties)ハブのプロパティを取得するにはコネクタを選択します。
 
## <a name="6-client-deregistration"></a>6:クライアントの登録解除します。 
1. クライアント ドライバーの呼び出し[ **UsbPm_Deregister** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/usbpmapi/nf-usbpmapi-usbpm_register)通知が不要になったドライバーに必要がある場合。
2. Policy Manager の登録を解除するクライアント ハンドルの登録をマークおよびは呼び出しません**EVT_USBPM_EVENT_CALLBACK**コールバック。

## <a name="see-also"></a>参照

[USB タイプ-c コネクタのドライバーを作成します。](https://docs.microsoft.com/windows-hardware/drivers/usbcon/bring-up-a-usb-type-c-connector-on-a-windows-system)

[USB タイプ-c ポート コント ローラー ドライバーを作成します。](https://docs.microsoft.com/windows-hardware/drivers/usbcon/write-a-usb-type-c-port-controller-driver)

[USB 関数コント ローラーのクライアント ドライバーを記述します。](https://docs.microsoft.com/windows-hardware/drivers/usbcon/function-client-driver)
