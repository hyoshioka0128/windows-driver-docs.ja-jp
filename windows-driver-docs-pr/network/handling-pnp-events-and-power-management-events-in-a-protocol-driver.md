---
title: PnP の処理とプロトコル ドライバーで電源管理イベント
description: プロトコル ドライバーの PnP イベントと電源管理イベントの処理
ms.assetid: 97cc51f1-7d83-4bf1-87e3-7d986f54e7a1
keywords:
- プロトコル ドライバー WDK ネットワーク、電源管理
- NDIS プロトコル ドライバー WDK、電源管理
- プロトコル ドライバー WDK ネットワー キング、プラグ アンド プレイ
- NDIS プロトコル ドライバー WDK、プラグ アンド プレイ
- 電源管理 WDK NDIS プロトコル
- プラグ アンド プレイ WDK NDIS プロトコル
- WDK PnP、NDIS プロトコル ドライバーに通知
- イベント通知の WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b3d38c6f612a38054b2b3b3eeb2fb05aa62f9d9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379792"
---
# <a name="handling-pnp-events-and-power-management-events-in-a-protocol-driver"></a>プロトコル ドライバーの PnP イベントと電源管理イベントの処理

オペレーティング システムでは、プラグ アンド プレイ (PnP) I/O 要求パケット (IRP) または電源管理 IRP がネットワーク インターフェイス カード (NIC) を表すターゲット デバイス オブジェクトを発行、NDIS は IRP をインターセプトします。 NDIS を呼び出してドライバーの各バインド プロトコル ドライバーとバインドされた各中間ドライバーにイベントを示します[ *ProtocolNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event)関数。 呼び出しで*ProtocolNetPnPEvent*、NDIS へのポインターを渡す、 [ **NET\_PNP\_イベント\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_pnp_event_notification)を格納しています。NET\_PNP\_イベント構造体。 NET\_PNP\_PnP イベントまたは指定されている電源管理イベント、イベントの構造について説明します。 プロトコル ドライバーの PnP インターフェイスの詳細については、次を参照してください。[プロトコル ドライバーでの PnP イベント通知の処理](handling-pnp-event-notifications-in-a-protocol-driver.md)します。

示されている、PnP や電源管理イベントの一覧を次の**NetEvent**ネット コード\_PNP\_イベントの構造。

-   **NetEventSetPower**

    ミニポート アダプターが、特定の電源の状態に移行する必要があることを指定します、電源の設定の要求を示します。 電源管理に対応したプロトコルのドライバーが NDIS を返すことによってこのイベントを常に成功する必要があります\_状態\_成功します。 古いプロトコル ドライバーは、NDIS を返すことができます\_状態\_いない\_NDIS はミニポート アダプターからこれにバインドを示すには、サポートされています。

    セットの電力の要求を発行した後は、NDIS はミニポート アダプターが低電力状態に遷移する場合に、ドライバー スタックを一時停止します。 NDIS は、ミニポート アダプターが (D0) の作業の状態に遷移する場合に、省電力要求の前に、ドライバー スタックを再起動します。 一時停止して再起動ドライバー スタックの詳細については、次を参照してください。[ドライバー スタックを一時停止](pausing-a-driver-stack.md)します。

    ミニポート アダプターが低電力状態にある場合、プロトコル ドライバーには、OID 要求を発行できません。 この要件は、ドライバー スタックが一時停止状態のときに適用されるその他の制限に追加される追加の電源管理の制限です。

    場合は、基になるミニポート アダプタの管理に対応した電源は、ミニポート ドライバーの設定、**デバイス**のメンバー [ **NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)に**NULL**と NDIS セット、**デバイス**のメンバー [**NDIS\_バインド\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)に**NULL**します。

    **注**NDIS 6.30、以降、このイベントの通知を送信プロトコル ドライバーは新しい I/O 要求の生成を停止する必要があり、保留中の I/O 要求への呼び出しのコンテキスト内での完了を待つ必要がありますいない[ *ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event)します。

    セット電源イベントの詳細については、次を参照してください。 [PnP イベントを処理し、中間のドライバーで電源管理イベント](handling-pnp-events-and-power-management-events-in-an-intermediate-dri.md)します。

-   **NetEventQueryPower**

    クエリ機能要求、クエリは、基になるミニポート アダプターは特定の電源状態に遷移を作成できるかどうかを示します。 プロトコル ドライバーは常に成功する必要があります、 **NetEventQueryPower**します。 アクティブな接続を確立した後、プロトコルのドライバーを呼び出すことができます[ **PoRegisterSystemState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-poregistersystemstate)を継続的なビジー状態を登録します。 状態の登録を有効になっている限り、電源マネージャーしようとしませんシステムをスリープ状態を格納します。 プロトコル ドライバーが呼び出すことによって状態登録をキャンセル、接続が非アクティブになった後[ **PoUnregisterSystemState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-pounregistersystemstate)します。 プロトコル ドライバーは、システムが失敗したことでスリープ状態に遷移するを防ぐためにしないでください、 **NetEventQueryRemoveDevice**します。 なお、 **NetEventQueryPower**が常に続く、 **NetEventSetPower**します。 A **NetEventSetPower**するセット、デバイスの現在の電源状態有効取り消さ、 **NetEventQueryPower**します。

    **注**NDIS 6.30、以降、このイベントの通知を送信しますプロトコル ドライバーにする必要がありますいない完了を待つ、保留中の I/O 要求への呼び出しのコンテキスト内での[ *ProtocolNetPnPEvent*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event).

-   **NetEventQueryRemoveDevice**

    クエリの デバイスの削除要求、クエリは、操作を中断することがなく、NIC を削除できるかどうかを示します。 場合プロトコル ドライバーは、デバイスを解放できません (たとえば、デバイス使用されているため)、失敗することが必要があります、 **NetEventQueryRemoveDevice** NDIS を返すことによって\_状態\_失敗します。

-   **NetEventCancelRemoveDevice**

    基になる NIC の削除がキャンセルされるデバイスの削除の取り消しの要求を示します NDIS を返すことによってこのイベントを常に成功する必要がありますプロトコル ドライバー\_状態\_成功します。

-   **NetEventReconfigure**

    ネットワーク コンポーネントの構成が変更されたことを示します。 たとえば、ユーザーは、TCP/IP の IP アドレスを変更する NDIS は このイベントを使用して、TCP/IP プロトコルを示します、 **NetEventReconfigure**コード。 プロトコル ドライバー、まれな状況は、エラー コードを返すことが示された構成の変更を適用できないと、使用可能な既定値がない場合。 メモリの割り当てに失敗した場合は、プロトコルにエラー コードが返されますの例に示します。 エラー コードを返すと、システムを再起動するように求めることができます。

    プロトコルを検証する必要があります**NetEventReconfigure**-に関連するデータが渡されるその[ *ProtocolNetPnPEvent* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_net_pnp_event)関数。 このようなデータの詳細については、次を参照してください。 [ **NET\_PNP\_イベント プロトコル ドライバーを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_pnp_event)します。

-   **NetEventBindList**

    プロトコル ドライバーにそのバインドの一覧の処理順序が再構成されていることを示します。 この一覧では、たとえば、複数のバインドのいずれかにルーティングすることも、ユーザーの要求を処理する際、プロトコルのバインドに適用する相対順序を示します。 このイベントに渡されたバッファーには、デバイス名が NULL で終わる Unicode 文字列として書式設定の一覧が含まれています。 各デバイス名の形式と同じですが、 *DeviceName*への呼び出しに渡されるパラメーター [ *ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)します。

    プロトコルを検証する必要があります**NetEventBindList**-に関連するデータが渡されるその*ProtocolNetPnPEvent*関数。 このようなデータの詳細については、次を参照してください。 [ **NET\_PNP\_イベント プロトコル ドライバーを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_pnp_event)します。

    プロトコルを検証する必要があります**NetEventBindList**-に関連するデータが渡されるその*ProtocolNetPnPEvent*関数。 このようなデータの詳細については、次を参照してください。 [ **NET\_PNP\_イベント プロトコル ドライバーを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_pnp_event)します。

-   **NetEventBindsComplete**

    プロトコル ドライバーにバインドできるすべての Nic にバインドされていることを示します。 しない限り、PnP NIC をシステムに接続するなど、NDIS はプロトコル ドライバーに複数のバインドを示していません。

-   **NetEventPnPCapabilities**

    ユーザーが有効になっているか、基になるアダプターのウェイク アップ機能を無効になっていることを示します。 (、 *ProtocolBindingContext* NDIS からに渡されるパラメーター *ProtocolNetPnPEvent*バインディングを指定します)。

-   **NetEventPause**

    指定したプロトコルのバインドが thePausing 状態を入力する必要がありますを示します。 NDIS は、すべてのバインディングの未処理の送信要求が完了した後、バインドは一時停止状態を入力します。 バインディングを一時停止の詳細については、次を参照してください。[バインディングを一時停止](pausing-a-binding.md)します。

-   **NetEventRestart**

    指定したプロトコルのバインドが再開中の状態を入力したことを示します。 バインディングは、プロトコル ドライバーの送信を再開およびバインディングの操作を受信する準備が実行中の状態が入力されます。 バインディングを再開する方法の詳細については、次を参照してください。[バインディングを再起動する](restarting-a-binding.md)します。

-   **NetEventPortActivation**

    指定したバインディングに関連付けられているポートの一覧のアクティブ化を示します。 バインディングを一時停止の詳細については、次を参照してください。[ポート アクティベーション PnP イベントを処理する](handling-the-port-activation-pnp-event.md)します。

-   **NetEventPortDeactivation**

    指定したバインディングに関連付けられているポートの一覧の非アクティブ化を示します。 バインディングを一時停止の詳細については、次を参照してください。[ポート非アクティブ化の PnP イベントを処理する](handling-the-port-deactivation-pnp-event.md)します。

-   **NetEventIMReEnableDevice**

    NDIS 6.0 または中間の以降のバージョンのドライバーの仮想ミニポートの構成が変更されたことを示します。 **NetEventIMReEnableDevice**に似ていますが、 **NetEventReconfigure**イベント中間ドライバーが 1 つの仮想ミニポートにこのイベントを受信する点を除いて、 **NetEventReconfigure**イベントが仮想ミニポートのドライバーの中間のすべてに適用されます。 たとえば、中間のドライバーの受信、 **NetEventIMReEnableDevice**ときに、ユーザーを無効にし、デバイス マネージャーまたは別のソースから 1 つの仮想ミニポート イベント。 中間ドライバーの電源管理の例については、次を参照してください。、 [NDIS MUX 中間ドライバーとオブジェクトの通知](https://go.microsoft.com/fwlink/p/?LinkId=617916)ドライバーのサンプルで使用できる、 [Windows ドライバー サンプル](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub リポジトリにあります。

**バッファー** net メンバー\_PNP\_イベントの構造が指定されているイベントに固有の情報を格納しているバッファーを指します。

プロトコル ドライバーへの呼び出しを完了できる*ProtocolNetPnPEvent*に非同期で[ **NdisCompleteNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscompletenetpnpevent)します。