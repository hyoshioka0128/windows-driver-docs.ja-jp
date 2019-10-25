---
title: 仮想ステーション
description: 仮想ステーション
ms.assetid: 6228439c-4c01-4fa9-8b45-b46ed90fa661
keywords:
- 仮想ステーションの WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a227b38ada98b9a724216569bc7a888c994645a4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842947"
---
# <a name="virtual-station"></a>仮想ステーション




 

NDIS 6.20 (Windows 7) 以降では、オペレーティングシステムは、802.11 ミニポートドライバーと対話できる仮想ステーション (VSTA) を提供します。

独立系ハードウェアベンダー (IHV) は、Win32 アプリケーションプログラミングインターフェイス (Api) ではなく、 [Ihv 拡張フレームワーク](overview-of-ihv-extensibility.md)を介して VSTA 機能を使用します。

IHV Extensions DLL が[**Dot11ExtRequestVirtualStation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_request_virtual_station)関数を呼び出すと、仮想ステーションの作成が開始されます。 オペレーティングシステムは、コンピューター上に一度に1つの仮想ステーションだけを作成します。また、IHV 拡張 DLL が**Dot11ExtRequestVirtualStation**要求を発行する場合にのみ作成します。

オペレーティングシステムは[*Dot11ExtIhvInitVirtualStation*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_init_virtual_station)関数を呼び出して、仮想ステーションの操作用に IHV 拡張 DLL を初期化します。 この呼び出しでは、オペレーティングシステムと DLL の間のユーザーモード API インターフェイスも初期化されます。

**注**  仮想ステーションが一貫した方法で作成されていることを確認するために、コンピューターには、仮想ステーションの機能を使用しようとする IHV 拡張 DLL を1つだけインストールする必要があります。 複数の DLL がインストールされている場合でも、作成できる仮想ステーションは1つだけです。 オペレーティングシステムは、コンピューターの再起動後にどの DLL が仮想ステーションにアクセスできるかを保証することはできません。 仮想ステーションが1つの DLL の要求で既に作成されていて、2番目の DLL が**Dot11ExtRequestVirtualStation**を呼び出すと、成功コードが返されますが、2つ目の仮想ステーションは作成されないことに注意してください。
IHV 拡張 DLL は、 **Dot11ExtRequestVirtualStation**関数を呼び出した後、2分のタイマーを設定する必要があります。 仮想ステーションアダプターの到着イベントの前にタイマーが期限切れになった場合、DLL は仮想ステーションが作成されていないと想定する必要があります。

 

### <a href="" id="extensible-ap-virtual-station-interactions"></a>拡張可能な AP/仮想ステーションの相互作用

ドライバーに仮想ステーション機能が実装されていても、[拡張アクセスポイント (ExtAP)](extensible-access-point-operation-mode.md)と仮想ステーションの両方の接続を異なるポートで同時に維持できない場合、ドライバーは次の操作を実行する必要があります。

-   ExtAP に使用されているポートが常に機能を維持できるかどうかをオペレーティングシステムに通知します。 特に、ドライバーは、適切な状態コード ( [**NDIS\_ステータス\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)表示-&gt;**StatusCode**) と理由コードを使用して、extap ポートで次の状態の表示を発行する必要があります。

    <a href="" id="ndis-status-dot11-stop-ap"></a>[NDIS\_STATUS\_DOT11\_\_AP の停止](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-dot11-stop-ap)  
    AP 機能を ExtAP ポートで維持できないことを示します。 この場合は、 [**dot11\_stop\_ap\_パラメーター**](https://docs.microsoft.com/windows-hardware/drivers/ddi/windot11/ns-windot11-_dot11_stop_ap_parameters)-&gt; **ULREASON**を DOT11\_停止\_AP\_\_をアクティブにします。 次の状況で、この状態の表示を発行します。

    -   仮想ステーションポートが、同時仮想ステーションと ExtAP 接続をブロックする共有リソースの使用を開始する前
    -   ExtAP ポートが ExtAP INIT 状態に遷移し、仮想ステーションのリソース使用によって ExtAP ポートが正常に初期化されない場合。

    <a href="" id="---------ndis-status-dot11-can-sustain-ap"></a>[NDIS\_の状態\_DOT11\_は\_AP を維持\_ことができます](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-dot11-can-sustain-ap)  
    仮想ステーションのポートが切断されていること、または仮想ステーションリソースを使用することによってポートが ExtAP INIT 状態に正常に移行できないことを示します。

-   仮想ステーションのポートに接続しているときに、 [**Dot11ExtSetVirtualStationAPProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_virtual_station_ap_properties)関数を呼び出して、仮想ステーション接続でホストされている AP 実装に関する情報を提供します。

-   ExtAP ポートが OP 状態で実行されていて、次のいずれかの状況が発生した場合、仮想ステーションのポート接続を失敗とします。
    -   1つ以上のクライアントが ExtAP ポート上にあります。
    -   仮想ステーションは、[ワイヤレスでホスト](https://go.microsoft.com/fwlink/p/?linkid=152328)されるネットワーク設定を複製する接続を開始しようとします。

### <a href="" id="native-802-11-ihv-extensibility-functions-that-support-a-virtual-stati"></a>仮想ステーションをサポートするネイティブ 802.11 IHV 拡張関数

[**Dot11ExtQueryVirtualStationProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_query_virtual_station_properties)

[**Dot11ExtReleaseVirtualStation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_release_virtual_station)

[**Dot11ExtRequestVirtualStation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_request_virtual_station)

[**Dot11ExtSetVirtualStationAPProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_virtual_station_ap_properties)

### <a href="" id="structures-that-support-a-virtual-station"></a>仮想ステーションをサポートする構造

[**DOT11EXT\_仮想\_ステーション\_AP\_プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_virtual_station_ap_property)

[**DOT11EXT\_仮想\_ステーション\_API**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_virtual_station_apis)

 

 





