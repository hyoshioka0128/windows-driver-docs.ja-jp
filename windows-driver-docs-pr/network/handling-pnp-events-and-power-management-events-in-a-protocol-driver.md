---
title: プロトコルドライバーでの PnP および電源管理イベントの処理
description: プロトコル ドライバーの PnP イベントと電源管理イベントの処理
ms.assetid: 97cc51f1-7d83-4bf1-87e3-7d986f54e7a1
keywords:
- プロトコルドライバー WDK ネットワーク、電源管理
- NDIS プロトコルドライバー WDK、電源管理
- プロトコルドライバー WDK ネットワーク、プラグアンドプレイ
- NDIS プロトコルドライバー WDK、プラグアンドプレイ
- 電源管理 WDK NDIS プロトコル
- プラグアンドプレイ WDK NDIS プロトコル
- 通知 WDK PnP, NDIS プロトコルドライバー
- イベント通知の WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a2bb96056020ac10c590d9b8dc48d5c17a44900
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842568"
---
# <a name="handling-pnp-events-and-power-management-events-in-a-protocol-driver"></a>プロトコル ドライバーの PnP イベントと電源管理イベントの処理

オペレーティングシステムが、ネットワークインターフェイスカード (NIC) を表すターゲットデバイスオブジェクトに対して、プラグアンドプレイ (PnP) i/o 要求パケット (IRP) または電源管理 IRP を発行すると、NDIS は IRP をインターセプトします。 NDIS は、ドライバーの[*ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)関数を呼び出すことによって、バインドされた各プロトコルドライバーとバインドされた中間ドライバーにイベントを示します。 *ProtocolNetPnPEvent*の呼び出しでは、NDIS は、NET\_PNP\_イベント構造を含む[ **\_通知\_net\_PNP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event_notification)にポインターを渡します。 NET\_PNP\_イベント構造は、示されている PnP イベントまたは電源管理イベントを表します。 プロトコルドライバーの PnP インターフェイスの詳細については、「[プロトコルドライバーでの Pnp イベント通知の処理](handling-pnp-event-notifications-in-a-protocol-driver.md)」を参照してください。

次の一覧には、ネットワーク\_PNP\_イベント構造の**Netevent**コードに示されているように、pnp および電源管理イベントが含まれています。

-   **NetEventSetPower**

    電源要求の設定を示します。これは、ミニポートアダプターを特定の電源状態に切り替える必要があることを指定します。 電源管理対応プロトコルドライバーは、NDIS\_STATUS\_SUCCESS を返すことによって、常にこのイベントを成功させる必要があります。 古いプロトコルドライバーは NDIS\_ステータス\_返すことができ\_サポートされていないため、NDIS がミニポートアダプターからバインド解除する必要があることを示しています。

    Set パワー要求を発行した後、ミニポートアダプターが低電力状態に移行している場合、NDIS はドライバースタックを一時停止します。 ミニポートアダプターが動作状態 (D0) に移行している場合、NDIS は、セットパワー要求の前にドライバースタックを再起動します。 ドライバースタックの一時停止と再起動の詳細については、「[ドライバースタックの一時停止](pausing-a-driver-stack.md)」を参照してください。

    ミニポートアダプターが低電力状態の場合、プロトコルドライバーは OID 要求を発行できません。 この要件は、ドライバースタックが一時停止状態のときに適用されるその他の制限に追加される追加の電源管理制限です。

    基になるミニポートアダプターが電源管理に対応していない場合、ミニポートドライバーは、 [**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)の**PowerManagementCapabilities**メンバーを**NULL**に設定し、NDIS は、\_パラメーターを**NULL**に[**バインド\_、ndis**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)の**PowerManagementCapabilities**メンバーを設定します。

    **メモ** NDIS 6.30 以降では、このイベントが通知された後、プロトコルドライバーは新しい i/o 要求の生成を停止する必要があり、 [*ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)への呼び出しのコンテキスト内で保留中の i/o 要求が完了するまで待機することはできません。

    セットパワーイベントの詳細については、「[中間ドライバーでの PnP イベントと電源管理イベントの処理](handling-pnp-events-and-power-management-events-in-an-intermediate-dri.md)」を参照してください。

-   **NetEventQueryPower**

    クエリの電源要求を示します。これは、基になるミニポートアダプターが特定の電源状態に移行できるかどうかを照会します。 プロトコルドライバーは、常に**NetEventQueryPower**に成功する必要があります。 アクティブな接続を確立すると、プロトコルドライバーは[**PoRegisterSystemState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-poregistersystemstate)を呼び出して、継続的なビジー状態を登録できます。 状態の登録が有効になっている限り、電源マネージャーはシステムをスリープ状態にしません。 接続が非アクティブになると、プロトコルドライバーは[**Pounregistersystemstate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pounregistersystemstate)を呼び出すことによって状態の登録を取り消します。 プロトコルドライバーは、 **NetEventQueryRemoveDevice**の失敗によってシステムがスリープ状態に移行しないようにする必要があります。 **NetEventQueryPower**の後に常に**NetEventSetPower**が続くことに注意してください。 デバイスの現在の電源状態を設定する**NetEventSetPower**は、 **NetEventQueryPower**を取り消します。

    **メモ** NDIS 6.30 以降では、このイベントが通知された後、 [*ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)の呼び出しのコンテキスト内で保留中の i/o 要求が完了するまで、プロトコルドライバーは待機しません。

-   **NetEventQueryRemoveDevice**

    操作を中断せずに NIC を削除できるかどうかをクエリする、デバイスの削除要求を示します。 たとえば、デバイスが使用中であるために、プロトコルドライバーがデバイスを解放できない場合は、NDIS\_STATUS\_のエラーを返すことによって**NetEventQueryRemoveDevice**を失敗させる必要があります。

-   **NetEventCancelRemoveDevice**

    デバイスの削除要求の取り消しを示します。これにより、基になる NIC の削除が取り消されます。 プロトコルドライバーは、NDIS\_STATUS\_SUCCESS を返すことによって、常にこのイベントを成功させる必要があります。

-   **NetEventReconfigure**

    ネットワークコンポーネントの構成が変更されたことを示します。 たとえば、ユーザーが TCP/IP の IP アドレスを変更した場合、NDIS は**NetEventReconfigure**コードを使用してこのイベントを tcp/ip プロトコルに示します。 プロトコルドライバーは、指定された構成の変更を適用できず、使用可能な既定値がない場合に、エラーコードを返すことがあります。 メモリを割り当てようとして失敗した場合の例として、プロトコルがエラーコードを返した場合が挙げられます。 エラーコードを返すと、ユーザーにシステムの再起動を求めるメッセージが表示されることがあります。

    プロトコルでは、 [*ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event)関数に渡される**NetEventReconfigure**関連のデータを検証する必要があります。 このようなデータの詳細については、「 [**NET\_PNP\_イベント (プロトコルドライバー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event))」を参照してください。

-   **NetEventBindList**

    プロトコルドライバーに、バインドリストの処理順序が再構成されたことを示します。 この一覧は、たとえば、複数のバインドのいずれかにルーティングされる可能性があるユーザー要求などの処理時に、プロトコルのバインドに適用される相対的な順序を示します。 このイベントと共に渡されるバッファーには、NULL で終わる Unicode 文字列として書式設定されたデバイス名の一覧が含まれています。 各デバイス名の形式は、 [*Protocolbindadapterex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)への呼び出しに渡される*DeviceName*パラメーターと同じです。

    プロトコルでは、 *ProtocolNetPnPEvent*関数に渡される**NetEventBindList**関連のデータを検証する必要があります。 このようなデータの詳細については、「 [**NET\_PNP\_イベント (プロトコルドライバー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event))」を参照してください。

    プロトコルでは、 *ProtocolNetPnPEvent*関数に渡される**NetEventBindList**関連のデータを検証する必要があります。 このようなデータの詳細については、「 [**NET\_PNP\_イベント (プロトコルドライバー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event))」を参照してください。

-   **NetEventBindsComplete**

    プロトコルドライバーがバインドできるすべての Nic にバインドされていることを示します。 たとえば、PnP NIC がシステムに接続されている場合を除き、プロトコルドライバーへのバインドは、NDIS によって示されません。

-   **NetEventPnPCapabilities**

    ユーザーが基になるアダプターのウェイクアップ機能を有効または無効にしたことを示します。 (NDIS が*ProtocolNetPnPEvent*に渡す*ProtocolBindingContext*パラメーターは、バインドを指定します。)

-   **NetEventPause**

    指定されたプロトコルバインドが一時停止状態になることを示します。 バインドに対する未処理の送信要求がすべて NDIS によって完了すると、バインドは一時停止状態になります。 バインディングの一時停止の詳細については、「[バインディングの一時停止](pausing-a-binding.md)」を参照してください。

-   **NetEventRestart**

    指定されたプロトコルバインドが再開中の状態になったことを示します。 プロトコルドライバーがバインディングの送信および受信操作を再開する準備ができたら、バインドは実行中の状態になります。 バインディングの再起動の詳細については、「[バインディングの再起動](restarting-a-binding.md)」を参照してください。

-   **NetEventPortActivation**

    指定したバインディングに関連付けられているポートのリストのアクティブ化を示します。 バインディングの一時停止の詳細については、「[ポートのアクティブ化 PnP イベントの処理](handling-the-port-activation-pnp-event.md)」を参照してください。

-   **NetEventPortDeactivation**

    指定したバインディングに関連付けられているポートのリストの非アクティブ化を示します。 バインディングの一時停止の詳細については、「[ポートの非アクティブ化の PnP イベントの処理](handling-the-port-deactivation-pnp-event.md)」を参照してください。

-   **NetEventIMReEnableDevice**

    NDIS 6.0 以降の中間ドライバーの仮想ミニポートの構成が変更されたことを示します。 **NetEventIMReEnableDevice**は**NetEventReconfigure**イベントに似ていますが、中間ドライバーが1つの仮想ミニポートに対してこのイベントを受信し、 **NetEventReconfigure**イベントがすべての中間に適用される点が異なります。ドライバーの仮想ミニポート。 たとえば、中間ドライバーは、ユーザーがデバイスマネージャーまたは別のソースから1つの仮想ミニポートを無効にしてから有効にすると、 **NetEventIMReEnableDevice**イベントを受け取ります。 中間ドライバーの電源管理の例については、GitHub の[Windows ドライバーのサンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507)リポジトリにある[NDIS MUX 中間ドライバーと通知オブジェクト](https://go.microsoft.com/fwlink/p/?LinkId=617916)ドライバーのサンプルを参照してください。

NET\_PNP\_イベント構造の**バッファー**メンバーは、示されているイベントに固有の情報を含むバッファーを指します。

プロトコルドライバーは、 [**NdisCompleteNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscompletenetpnpevent)を使用して*ProtocolNetPnPEvent*への呼び出しを非同期に完了できます。