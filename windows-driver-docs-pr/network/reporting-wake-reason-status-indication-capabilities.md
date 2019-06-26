---
title: NDIS ウェイク理由状態表示機能のレポート
description: NDIS ウェイク理由状態表示機能のレポート
ms.assetid: A72D04F7-EB09-4B1B-9AF5-7FEBC2514CE9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d921fabd2b254509014e5f30cc2ac2992777582
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373231"
---
# <a name="reporting-wake-reason-status-indication-capabilities"></a>NDIS ウェイク理由状態表示機能のレポート


NDIS 6.30 以降、ミニポート ドライバー報告する必要がある NDIS ウェイク アップの理由の状態を示す値を発行できるかどうか ([**NDIS\_状態\_PM\_WAKE\_理由**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason))、次のいずれかによって発生したウェイク アップのイベントを報告します。

-   ネットワーク アダプターは、wake on LAN (WOL) のパターンに一致するパケットを受信しました。 オブジェクト識別子 (OID) セット要求で指定された受信フィルターに一致するパケットの受信が含まれます[OID\_GEN\_現在\_パケット\_フィルター](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-current-packet-filter)します。

    **注**  この種類のウェイク アップの理由の状態の表示にするは、ネットワーク アダプターで受信したパケットを保存できる必要があります。 ドライバーは、受信パケット内の状態を示す値を返す必要があります。

     

-   ネットワーク アダプターには、802.11 アクセス ポイント (AP) またはモバイル ブロード バンド (MB) のショート メッセージ サービス (SMS) メッセージの受信から関連付け解除などのメディア固有のイベントが検出されました。

-   ネットワーク アダプターが、WOL パターンに固有ではない別の有効なイベントを検出またはメディアの種類 (*メディアに依存しないイベント*)。 ミニポート ドライバーの問題など、 [ **NDIS\_状態\_PM\_WAKE\_理由**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)ネットワーク アダプターを有効になっている場合、状態の表示メディア接続または切断を検出します。

**注**  サポートの NDIS ウェイク状態インジケーターの理由の指定はモバイル ブロード バンド (MB) のミニポート ドライバーでは省略可能。

 

NDIS がドライバーを呼び出すときに[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)次の手順に従って関数、ミニポート ドライバーのレポートのスリープ解除理由の状態を示す値機能。

1.  ミニポート ドライバーを初期化します、 [ **NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_capabilities)基になるハードウェアの電源管理機能を含む構造体。

    ウェイク アップの理由の状態インジケーターのサポートを有効にする、ミニポート ドライバーがのメンバーを設定する必要があります、 [ **NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_capabilities)次のように構造体します。

    -   NDIS ミニポート ドライバーを指定してください\_PM\_機能\_リビジョン\_2 および NDIS\_SIZEOF\_NDIS\_PM\_機能\_リビジョン\_リビジョンと長さの 2、 [ **NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_capabilities)の構造体の内部構造**ヘッダー**メンバー。
    -   ミニポート ドライバーが、NDIS を設定する場合は、ネットワーク アダプターには、システムのウェイク アップ イベントの原因となった受信パケットを格納できる、\_PM\_WAKE\_パケット\_INDICATION\_内でサポートされているフラグ**フラグ**この構造体のメンバー。

        このフラグが設定されている場合、ネットワーク アダプターはアダプターが、ウェイク アップのイベントを生成する原因となった受信パケットを保存できる必要があります。 さらに、ミニポート ドライバーは、このパケットを使用して、ネットワークの後に次の電力状態に遷移をアダプターを実行できる必要があります。

        -   呼び出すことによって、パケットを示すために、ミニポート ドライバーがあります[ **NdisMIndicateReceiveNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatereceivenetbufferlists)します。

        -   ミニポート ドライバーで発行できる必要があります、 [ **NDIS\_状態\_PM\_WAKE\_理由**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-pm-wake-reason)状態を示す値を持つパケットを渡す必要があります、示します。

    -   ミニポート ドライバーのセット、 **MaxWoLPacketSaveBuffer**メンバーのシステムのウェイク アップ イベントの原因となった、WOL パケットを格納しているバッファーのバイト単位の最大サイズにします。

        値、 **MaxWoLPacketSaveBuffer**メンバーには、最大転送単位 (MTU) のバイト単位のサイズを小さくする必要があり、メディア、メディアのネットワーク制御 (MAC) ヘッダーにアクセスします。 ドライバーの OID クエリ要求を通じた MTU サイズを報告する[OID\_GEN\_最大\_フレーム\_サイズ](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-maximum-frame-size)します。

    -   ミニポート ドライバーのセット、 **SupportedWakeUpEvents**メディアに依存しないウェイク アップ イベント、アダプターがネットワーク インターフェイスに接続されている場合は、ウェイク アップのイベントを生成するなど、ネットワーク アダプターをサポートします。

    -   ミニポート ドライバーのセット、 **MediaSpecificWakeUpEvents**ネットワーク アダプターをサポートするメディア固有のウェイク アップ イベントにします。 これらのイベントには、802.11 アダプターになります、AP との関連付けを解除する場合は、ウェイク アップのイベントの生成が含まれます。

2.  ミニポート ドライバーを初期化します、 [ **NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)構造と設定、**PowerManagementCapabilitiesEx**メンバーの初期化されたアドレスに[ **NDIS\_PM\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pm_capabilities)構造体。

3.  ミニポート ドライバーの呼び出し、 [ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)の電源管理機能を登録する関数。 ミニポート ドライバーでは、この関数を呼び出しとき、に、設定、 *MiniportAttributes*パラメーターのアドレスを[ **NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)構造体。

ウェイク アップの理由のステータスを示す値機能を報告するミニポート ドライバーによって使用されるメソッドは、電源管理機能を報告するための NDIS 6.20 が動作方法に基づきます。 この方法の詳細については、次を参照してください。[電源管理機能の報告](reporting-power-management-capabilities.md)します。

アダプターの初期化プロセスの詳細については、次を参照してください。[ミニポート アダプターの初期化](initializing-a-miniport-adapter.md)します。

電源管理機能のレポート方法の詳細については、次を参照してください。[電源管理機能の報告](reporting-power-management-capabilities.md)します。

 

 





