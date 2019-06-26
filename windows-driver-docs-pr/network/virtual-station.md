---
title: 仮想ステーション
description: 仮想ステーション
ms.assetid: 6228439c-4c01-4fa9-8b45-b46ed90fa661
keywords:
- WDK のステーションの仮想ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9356ca1c0a72164235e0d3aef3f55240c7dec39c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353628"
---
# <a name="virtual-station"></a>仮想ステーション




 

以降では、NDIS 6.20 (Windows 7) は、オペレーティング システムは、802.11 ミニポート ドライバーと対話できる仮想ステーション (VSTA) を提供します。

独立系ハードウェア ベンダー (IHV) を通じて VSTA 機能を使用して、 [IHV Extensibility framework](overview-of-ihv-extensibility.md)なくを通じて Win32 アプリケーション プログラミング インターフェイス (Api)。

IHV 拡張機能の DLL を呼び出すと、仮想ステーションの作成が開始される、 [ **Dot11ExtRequestVirtualStation** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_request_virtual_station)関数。 オペレーティング システム仮想ステーションを 1 つだけコンピューターの場合は、時刻、およびだけで、IHV 拡張機能の DLL を作成の問題、 **Dot11ExtRequestVirtualStation**要求。

オペレーティング システムの呼び出し、 [ *Dot11ExtIhvInitVirtualStation* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_init_virtual_station)仮想ステーション操作の IHV 拡張 DLL を初期化します。 この呼び出しはまた、オペレーティング システムと、DLL の間ユーザー モード API インターフェイスを初期化します。

**注**  仮想ステーションが一貫性のある方法で作成されたことを確認して、コンピューターの仮想ステーションの機能の使用を試みる IHV 拡張 DLL の 1 つだけインストール必要があります。 1 つ以上の DLL がインストールされている場合でも、1 つだけの仮想ステーションを作成できます。 オペレーティング システムで保証できないする DLL がアクセスを仮想ステーション、コンピューターの再起動後です。 仮想ステーション既に作成されている場合、要求の 1 つの DLL と 2 つ目の DLL にし、呼び出す**Dot11ExtRequestVirtualStation**、成功コードが返される可能性がありますが、2 つ目の仮想ステーションは作成されません。
呼び出された後、IHV の拡張 DLL は、2 分間タイマーを設定する必要があります、 **Dot11ExtRequestVirtualStation**関数。 ステーションの仮想アダプターの到着のイベントの前に、タイマーが切れるは仮想ステーションが作成されなかったことを DLL で想定してください。

 

### <a href="" id="extensible-ap-virtual-station-interactions"></a> 拡張可能なアジア太平洋/仮想ステーションの相互作用

かどうか、ドライバーでは仮想ステーションの機能を実装が、両方を維持することはできません[拡張可能なアクセス ポイント (ExtAP)](extensible-access-point-operation-mode.md)仮想ステーション接続と異なるポートを同時に、ドライバーが次の操作を実行する必要があります。

-   ExtAP の使用されているポートができますか、常に機能を維持することはできませんかオペレーティング システムに通知します。 具体的には、ドライバーが適切な状態コードを使用して ExtAP ポートでは、次の状態インジケーターを発行する必要があります ( [ **NDIS\_状態\_INDICATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication) - &gt; **StatusCode**) と、理由コード。

    <a href="" id="ndis-status-dot11-stop-ap"></a>[NDIS\_状態\_DOT11\_停止\_アジア太平洋](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-dot11-stop-ap)  
    ExtAP ポートでアジア太平洋の機能を維持することはできませんを示します。 この場合、設定[ **DOT11\_停止\_AP\_パラメーター** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/windot11/ns-windot11-_dot11_stop_ap_parameters) - &gt; **ulReason**の値をDOT11\_停止\_AP\_理由\_AP\_アクティブです。 次の状況でこの状態を示す値を発行します。

    -   仮想ステーションのポートは、同時仮想ステーションと ExtAP 接続を阻止する共有リソースの使用を開始する前に
    -   ExtAP INIT の状態とリソースの仮想ステーションに ExtAP ポート遷移を使用する場合は、ExtAP ポートの初期化の成功ができなくなります。

    <a href="" id="---------ndis-status-dot11-can-sustain-ap"></a>[NDIS\_状態\_DOT11\_できます\_サステイン\_アジア太平洋](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-dot11-can-sustain-ap)  
    仮想ステーションのポートが切断されているか、ExtAP 初期化状態、ポートの移行に成功を妨げません仮想ステーション リソースの使用することを示します。

-   ステーションの仮想ポートへの接続中に呼び出し、 [ **Dot11ExtSetVirtualStationAPProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_virtual_station_ap_properties)仮想ステーションでホストされているアジア太平洋の実装に関する情報を提供する関数接続します。

-   ExtAP ポートが OP 状態で実行されていると、次の状況のいずれかが発生した場合は、ステーションの仮想ポートの接続を失敗します。
    -   1 つまたは複数のクライアントは ExtAP ポートでは。
    -   重複する接続を開始しようとしている仮想ステーション[ワイヤレス ホスト ネットワーク](https://go.microsoft.com/fwlink/p/?linkid=152328)設定します。

### <a href="" id="native-802-11-ihv-extensibility-functions-that-support-a-virtual-stati"></a> 仮想ステーションをサポートするネイティブの 802.11 IHV 拡張関数

[**Dot11ExtQueryVirtualStationProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_query_virtual_station_properties)

[**Dot11ExtReleaseVirtualStation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_release_virtual_station)

[**Dot11ExtRequestVirtualStation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_request_virtual_station)

[**Dot11ExtSetVirtualStationAPProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11ext_set_virtual_station_ap_properties)

### <a href="" id="structures-that-support-a-virtual-station"></a> 仮想ステーションをサポートする構造体

[**DOT11EXT\_仮想\_ステーション\_AP\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/ns-wlanihv-_dot11ext_virtual_station_ap_property)

[**DOT11EXT\_仮想\_ステーション\_API**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/ns-wlanihv-_dot11ext_virtual_station_apis)

 

 





