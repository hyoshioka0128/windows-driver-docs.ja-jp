---
title: 接続状態の表示
description: 接続状態の表示
ms.assetid: 8a511c14-6b09-47fe-90de-6a90dab93171
keywords:
- WMI WDK ネットワーク, メディア接続の状態
- ミニポートドライバー WDK ネットワーク、メディア接続の状態
- NDIS ミニポートドライバー WDK、メディア接続の状態
- 接続ステータス WDK ネットワーク
- メディア接続 WDK ネットワーク
- NDIS_STATUS_MEDIA_CONNECT
- NDIS_STATUS_MEDIA_DISCONNECT
- ステータス情報 WDK NDIS ミニポート
- WDK ネットワーク、メディア接続の状態を示す状態
- 休止状態 WDK ネットワーク
- スリープ状態の WDK ネットワーク
- 状態 WDK ネットワークをリセットしています
- 状態 WDK ネットワークの停止
- 状態 WDK ネットワークを初期化しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27f9759419fcae3deedde11c1138063d2946a4d7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824706"
---
# <a name="indicating-connection-status"></a>接続状態の表示





ミニポートドライバーは、 [**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)または[**NdisMCoIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcoindicatestatusex)を呼び出して、メディア接続状態の変更を示します。 ミニポートドライバーは、 **Ndism (Co) IndicateStatus**に次のいずれかの状態を渡します。

<a href="" id="ndis-status-media-connect"></a>NDIS\_状態\_メディア\_接続  
メディア接続の状態が切断から接続に変更されたことを示します。 切断されたアダプターがネットワークに接続すると、メディア接続の状態が変化します。 たとえば、アダプターは、(ワイヤレスアダプターの) 範囲内にある場合、またはユーザーがネットワークケーブルを接続する場合に接続します。

<a href="" id="ndis-status-media-disconnect"></a>NDIS\_ステータス\_メディア\_切断  
メディア接続の状態が接続済みから切断済みに変更されたことを示します。 メディア切断状態の変更は、接続されているアダプターがネットワーク接続を失ったときに発生します。 たとえば、アダプターは、(ワイヤレスアダプターの) 範囲外にあるか、ユーザーがネットワークケーブルを unplugs しているため、接続を失います。

特に指定しない限り、ミニポートドライバーは、状態の変更を検出してから2秒以内にメディア接続の状態の変化を示す必要があります。

ミニポートドライバーは、特定の操作の実行中にメディア接続の状態を確認できます (次の一覧を参照してください)。 操作が開始されてから操作が完了した後に状態が同じ場合、ミニポートドライバーは、操作中に発生した可能性のある状態の変更を報告する必要がありません。

次の一覧では、ミニポートドライバーのメディア接続状態の変更を示す追加の要件について説明します。

<a href="" id="resetting"></a>戻す  
ミニポートドライバーをリセットするために、NDIS は[*Miniportresetex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)を呼び出します。 ミニポートドライバーは、同期または非同期のいずれかでリセットを完了できます。

リセット後にメディア接続の状態が異なる場合、ドライバーはリセットの完了後2秒以内に状態を示す必要があります。

ミニポートドライバーは、メディアの接続状態を確認するまで、リセット操作を完了できません。

<a href="" id="halting"></a>禁止  
ミニポートドライバーは、NDIS が[*ミニ Porthaltex*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_halt)を呼び出すときに、メディア接続の状態の変更を示すことはできません。

<a href="" id="initializing"></a>初期化  
NDIS は、ミニポートドライバーの[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)関数を呼び出して、アダプターを初期化します。 アダプターの初期化中に、ミニポートドライバーは次のガイドラインに従う必要があります。

-   *MiniportInitializeEx*から復帰した後、ミニポートドライバーがメディア接続の状態を示していない場合、Ndis は[**NDIS\_ミニポート\_アダプター\_全般\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)構造の**MediaConnectState**メンバーの値を使用して、メディアの接続状態を確認します。 ドライバーが*MiniportInitializeEx*関数から[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)を呼び出すと、ミニポートドライバーはこの構造を使用して NDIS を提供します。

    **注**  **MediaConnectState**メンバーが MediaConnectStateUnknown に設定されている場合、NDIS はアダプターが切断されているかのように処理を続行します。

     

-   NDIS が*MiniportInitializeEx*を呼び出した後、アダプターが接続されている場合、ミニポートドライバーは、 *MiniportInitializeEx*から戻ってから5秒以内に、NDIS\_ステータス\_メディア\_接続を示すことができます。

-   NDIS が*MiniportInitializeEx*を呼び出した後にアダプターが切断された場合、ミニポートドライバーは、 *MiniportInitializeEx*からの戻り後2秒以内にデバイス\_切断する NDIS\_ステータス\_を示す必要があります。

-   初期化中に、ミニポートドライバーは、 [oid\_gen\_media\_接続\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-media-connect-status)または[oid\_生成\_CO\_メディア\_接続\_状態](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-co-media-connect-status)要求を非同期に処理する必要があります。 ミニポートドライバーは、接続状態を確認するまで、このような要求を完了することはできません。

-   メディア接続の状態を決定するときに、初期化を遅らせないようにしてください。 必要に応じて、ミニポートドライバーは、 *MiniportInitializeEx*内の接続状態を確認するプロセスを開始し、後でプロセスを完了する必要があります。 たとえば、ミニポートドライバーは、アダプターに接続状態をポーリングするタイマーを設定できます。

-   逆シリアル化されたミニポートドライバーは、初期化中にメディアの切断を示すことができますが、シリアル化されたミニポートドライバーは使用できません。

<a href="" id="sleeping"></a>あっ  
ミニポートドライバーは、 [OID\_PNP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pnp-set-power)を受信したときにネットワークスリープ状態になり、\_電源要求を設定して、D1、D2、または D3 のデバイスの電源状態を設定する\_ます。

ミニポートドライバーは、スリープ状態に入ったとき、またはスリープ状態のときに、メディア接続状態の変化を示すことはできません。

<a href="" id="waking"></a>起き  
デバイスの電源状態を D0 に設定するために\_電源要求を受信すると、ミニポートドライバーは、OID\_\_PNP を受信したときにスリープ状態から復帰します。

スリープ解除後のメディア接続状態がスリープ状態の場合と同じである場合、ミニポートドライバーはメディア接続状態の変更を示すことはできません。 接続状態が変更された場合は、スリープ解除してから2秒以内に新しい接続状態をミニポートドライバーが示す必要があります。

スリープ状態のときに、ミニポートドライバーでは、OID\_GEN\_MEDIA\_接続\_状態または OID\_の生成\_の CO\_メディア\_非同期に接続する必要があります。\_ ミニポートドライバーは、接続状態を確認するまで、このような要求を完了することはできません。

 

 





