---
title: WDI TX パス
description: このセクションでは、WDI TX パスについて説明します。
ms.assetid: 8DF3E82E-761E-4A90-A789-1CB8EE8F0377
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51af368e4aabd1b6f01cd18a64f2a4579b2d96e2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841712"
---
# <a name="wdi-tx-path"></a>WDI TX パス


## <a name="tx-path-components"></a>TX パスコンポーネント


次の図は、TX パスのコンポーネントを示しています。

![wdi tx パス](images/wdi-tx-path-block-diagram.png)

## <a name="tx-descriptors"></a>TX 記述子


TAL は、ターゲットの TX 記述子 (TTD) を使用して、フレームのサイズと位置をターゲットに通知します。

ターゲット WLAN デバイスによって、TTD の定義が異なる場合があります。 このため、WDI によって提供される情報に基づいて、TTD プログラミングが TAL 内で行われます。 TTD をプログラミングするために、WDI は、フレーム ID、拡張 TID、適用可能なタスクオフロード、暗号化除外アクションなどのフレームメタデータにアクセスできる、 [**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) (NBL) を指定します。

TAL は、TTD と TX フレームをターゲットに転送します。 ターゲットは、フレームのヘッダー内の TTD およびフィールドのメタデータから、送信フレームの目的の受信者と送信方法を決定できます。

最終的には、ターゲットはフレームを送信し、転送 (および場合によっては転送) が行われたときにホストに通知します。 ターゲットでは、送信が成功したかどうかを指定する TX 完了メッセージと、送信が完了したフレームの Id を使用します。

## <a name="basic-operation"></a>基本操作


データフレームを送信するには、WLAN ホスト TX ソフトウェア内で次の手順を実行します。

1.  WDI は NDIS から NBL を取得し、TX 分類を実行します (WDI が PeerTID queuing モードで動作している場合)。
2.  NBL は、TAL に対してクエリを実行することで得られる TTD にリンクされます。 効率性を高めるために、TAL はルックアサイドリストから TTDs を事前に事前に割り当てることができます。
3.  TxMgr は、 **Target優先キュー**モードに応じて、peertid またはポートに基づいて送信フレームをキューに入れます。
4.  TxMgr は、NBL とアタッチされた TTD を Txmgr に提供します。これは、ターゲットに転送するために TIL に渡します。 TxEngine/TIL は、フレームをキューにしません (たとえば、DMA に使用できるようにする前など)。
5.  TxEngine は、転送の完了を使用して、TxEngine/ターゲットが所有するフレームの更新された TX ステータス (および該当する場合は送信完了を示す) を示します。
6.  フレームが転送完了 (必要に応じて、TX 完了) になると、TxMgr はフレーム ID を使用して NBL を検索し、TTD を Txmgr のプールに返して、フレームを NDIS に送信します。

## <a name="host---target-tx-flow-control"></a>ホスト-ターゲット TX フロー制御


TIL とターゲットリソースが過剰にならないようにするには、TX フロー制御が必要です。

### <a name="the-target-credit-scheme-and-the-pauseresume-mechanism"></a>ターゲットクレジットスキームと一時停止/再開メカニズム

TxMgr は、クレジットベースのスキームに従って、TX フレームをキューに登録し、ターゲットに転送します。 ターゲットは、発信先で追加のフレームに使用できるリソースを指定するクレジット更新の表示を提供します。 ターゲットの各フレームによって使用されるクレジットの数は、TTD のプログラミング時に決定されます。 指定されたキューからの送信操作の一部として TxEngine に渡されるフレーム数は、使用可能なクレジットと、行の先頭にあるフレームの FIFO 順序でのコストによって制限されます。

TxMgr には、クレジットに抽象単位があります。 ターゲット/TxEngine は、特定の実装にとって最も役に立つクレジットの定義をすべて使用する必要があります。

TAL は、一時停止/再開のインジケーターを使用して、指定されたポートからの TX トラフィックのフローを停止/再開したり、特定の TID を持つ特定の受信者宛てに送信したりします。 使用可能なクレジットが最大フレームコストよりも少ない場合に、TxEngine が送信要求を取得すると、TxEngine は、ターゲットからの次のクレジットの更新まで、Txengine からのトラフィック (すべてのポートで) を一時停止します。

WDI がポートキューモード (**Target優先キュー**に等しい場合) である場合、一時停止/再開のインジケーターは、ピア、TID 分類、およびキューがないため、ポートまたはアダプターレベルでのみ許可または定義されます。

### <a name="limiting-the-maximum-frame-count-for-send-operations"></a>送信操作の最大フレーム数の制限

TIL の一時キュー (たとえば、DMA レート照合キュー) が不要になるように、TxMgr が送信操作で Txmgr に渡すフレームの数は、Txmgr によって指定された最大数によって制限されます。 この制限は、TIL で使用可能な領域が増えるため、TxMgr が送信しようとしているキューと、時間の経過と共に変更される可能性があります。

## <a name="host---target-tx-transfer-scheduling"></a>ホストターゲットの TX 転送のスケジュール設定


TxMgr は、1つの TX スレッドを使用して、フレームを Txmgr に送信します。 バックログされたキューがある限り、TX スレッドは TxEngine にフレームをアクティブに送信しています。

TxMgr は、キューモードに応じて、次の方法でキューをスケジュールします。

WDI ポートキュー (**Target優先キュー**が TRUE) の場合、txmgr は、バックログされたすべてのポートキューで、不足ラウンドロビン (drr) を使用してキューをキューにします。

WDI peertid キュー (**接続 queuing**は FALSE) の場合、txmgr はキューを使用しない AC 優先度に従ってキューをキューに置いて、TIL とターゲット内のボトルネックに関するリソースが、適切な方法で RA tid ストリーム間で共有されることを保証します. これにより、低速のストリームがそのようなリソースを過度に共有するのを防ぐことができます。

一般に、スケジューラは、任意の時点で送信するピア TID キューを DRR を使用して選択します。 各キューについて、DRR は、各ラウンドでキューから送信するオクテット数を制限するクォンタムパラメーターを関連付けます。 TxEngine は、キューに関連する各送信操作でこのパラメーターを更新して、1つまたは2つの転送営業案件の予想サイズを一致させます。

一般に、DRR スケジューラは、最も高い優先順位のバックログ AC に関連付けられている RA TID キューのみをサービスします。 枯渇を防ぐために、スケジューラは、バックログされたすべてのキューで DRR を定期的に実行します。

### <a name="priority-mapping-for-ihv-reserved-extended-tids"></a>IHV 予約拡張 TIDs の優先順位マッピング

Ihv 予約範囲の拡張 TID で、IHV によって挿入されたフレームは、優先順位のスケジュール設定のために、次の拡張 ACs にマップされます。 テーブルの優先順位は高くなっています。

|              |        |        |        |        |         |         |         |         |
|--------------|--------|--------|--------|--------|---------|---------|---------|---------|
| 拡張 TID | 17     | 18     | 19     | 20     | 21      | 22      | 23      | 24      |
| 拡張 AC  | AC\_BK | AC\_ | AC\_VI | AC\_VO | AC\_PR0 | AC\_PR1-ASCS-0 | AC\_PR2 | AC\_PR3 |

 

WDI ポートキューの場合、挿入されたすべてのフレームは、拡張された TID に関係なく、同じように扱われます。

## <a name="txmgr-txengine-interface"></a>TxMgr-Txmgr インターフェイス


### <a name="requests-to-txengine"></a>TxEngine への要求

-   [*ミニポート\_WDI\_TX\_ABORT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_abort)
-   [*ミニポート\_WDI\_TX\_データ\_送信*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_data_send)
-   [*ミニポート\_WDI\_TX\_TAL\_キュー\_\_の順序*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_tal_queue_in_order)
-   [*ミニポート\_WDI\_TX\_TAL\_送信*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_tal_send)
-   [*ミニポート\_WDI\_TX\_TAL\_送信\_完了*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_tal_send_complete)
-   [*ミニポート\_WDI\_TX\_ターゲット\_DESC\_DEINIT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_target_desc_deinit)
-   [*ミニポート\_WDI\_TX\_ターゲット\_DESC\_INIT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_target_desc_init)

### <a name="indications-from-txengine"></a>TxEngine からの指示

-   [*NDIS\_WDI\_TX\_デキュー\_IND*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_dequeue_ind)
-   [*NDIS\_WDI\_TX\_転送\_完了\_IND*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_transfer_complete_ind)
-   [*NDIS\_WDI\_TX\_送信\_完了\_IND*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_send_complete_ind)
-   [*NDIS\_WDI\_TX\_クエリ\_RA\_TID\_状態*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_query_ra_tid_state)

### <a name="tx-specific-control-requests"></a>TX 固有の制御要求

-   [*ミニポート\_WDI\_TX\_ピア\_バックログ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_peer_backlog)

### <a name="tx-specific-control-indications"></a>TX 固有のコントロールのインジケーター

-   [*NDIS\_WDI\_TX\_送信\_一時停止\_IND*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_send_pause_ind)
-   [*NDIS\_WDI\_TX\_送信\_再起動\_IND*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_send_restart_ind)
-   [*NDIS\_WDI\_TX\_リリース\_フレーム\_IND*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_release_frames_ind)
-   [*NDIS\_WDI\_TX\_\_フレームの挿入\_IND*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-ndis_wdi_tx_inject_frame_ind)

## <a name="related-topics"></a>関連トピック


[WDI TX パス関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[**NET\_BUFFER\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)

[**WDI\_TXRX\_の機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_txrx_target_capabilities)

 

 






