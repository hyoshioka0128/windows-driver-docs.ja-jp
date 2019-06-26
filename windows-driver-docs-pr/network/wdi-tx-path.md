---
title: WDI TX パス
description: このセクションには、WDI TX パスがについて説明します
ms.assetid: 8DF3E82E-761E-4A90-A789-1CB8EE8F0377
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3556944f45e0e44eef30c9f2997b60c76e79cc00
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357107"
---
# <a name="wdi-tx-path"></a>WDI TX パス


## <a name="tx-path-components"></a>TX パス コンポーネント


次の図は、パス コンポーネントをテキサス州に示します。

![wdi tx path](images/wdi-tx-path-block-diagram.png)

## <a name="tx-descriptors"></a>TX 記述子


話してでは、ターゲット TX 記述子 (TTD) を使用して、サイズのターゲットとフレームの場所を通知します。

別のターゲットの WLAN のデバイス、TTD さまざまな定義があります。 このため、WDI によって提供される情報に基づいて、話して TTD プログラミングは実行できます。 TTD のプログラミング、WDI を指定します、 [ **NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list) (NBL) を通じて、フレームの ID など、フレームのメタデータ拡張 TID、適用可能なタスク オフロード、および暗号化除外対象のアクションは、アクセスできます。

ですかは、ターゲットに、TTD と TX フレームを転送します。 TTD とフレームのヘッダー内のフィールドのメタデータからターゲットに送信する方法と送信フレームの目的の受信者を判断できます。

最終的には、ターゲットは、フレームを送信し、転送 (および場合によって送信) が完了したら、ホストに通知します。 ターゲットは、テキサス州完了のメッセージ転送が成功したかどうかを指定してその転送が完了したフレームの Id を使用します。

## <a name="basic-operation"></a>基本的な操作


データ フレームを送信するには、WLAN ホスト TX ソフトウェア内で、次の手順が含まれます。

1.  WDI は、NDIS から、NBL を取得し、(WDI は PeerTID キュー モードで動作している) 場合は、テキサス州の分類を実行します。
2.  NBL は、クエリ、話してによって取得 TTD にリンクされます。 効率性を話してルック アサイド リストから TTDs あらかじめ割り当て可能性があります。
3.  キューに入れ、TxMgr PeerTID かに応じて、ポートに基づく送信フレーム、 **TargetPriorityQueueing**モード。
4.  TxMgr では、NBL と添付 TTD がターゲットに転送するための TIL に渡されます TxEngine を提供します。 TxEngine タイルはキューに登録 (たとえば、使用できるように DMA の) 前のフレーム/。
5.  TxEngine はフレーム転送の完了を使用して TxEngine/ターゲットによって所有されているの更新の TX 状態を示します (および、該当する場合は、完了を示す値を送信) します。
6.  フレームが完了すると両方の転送 (し、必要に応じて、TX 完了)、TxMgr 検索 NBL のフレーム ID を使用して、TxEngine を返します、TTD's プール、および NDIS にフレームを送信が完了します。

## <a name="host---target-tx-flow-control"></a>ホストが、送信フロー制御の対象


送信フロー制御は、TIL の混乱を回避し、ターゲット リソース必要があります。

### <a name="the-target-credit-scheme-and-the-pauseresume-mechanism"></a>ターゲット クレジット スキームと一時停止/再開の方法

クレジットに基づくスキームに従って、ターゲットに TxMgr キューと転送 TX フレームです。 ターゲットは、クレジット更新プログラムがないターゲットの追加のフレームの使用可能なリソースを指定すると、テキサス州エンジンを提供します。 ターゲット上の各フレームによって使用されるクレジット数が TTD プログラミング時に決定されます。 フレームの数は、特定のキューからの送信操作の一部が利用可能なクレジットと、FIFO の順序で行の先頭のフレームのコストが限られているために、TxEngine に渡されます。

クレジットでは、TxMgr に抽象のユニットがあります。 ターゲット/TxEngine では、クレジットの任意の定義は、特定の実装に最も役に立つを使用してください。

停止/再開、特定のポートからの送信トラフィックのフローを一時停止/再開の問題を使用してまたは特定 TID で特定の受信者に送信される、話してします。 利用可能なクレジットが最大フレーム コストより小さい、TxEngine 送信要求を取得します、TxEngine はターゲットから [次へ] のクレジット更新されるまで (すべてのポート) の間で TxMgr からのトラフィックを停止します。

WDI がポートのキュー モードの場合に (**TargetPriorityQueueing**が TRUE に等しい)、一時停止/再開の問題、許可されている定義でのみピア、TID の分類がないのため、ポートまたはアダプターのレベルとキューします。

### <a name="limiting-the-maximum-frame-count-for-send-operations"></a>送信操作の最大フレーム数を制限します。

(たとえば、キューに一致する DMA レート) TIL で一時的なキューの必要性を避けるためには、フレーム TxMgr に渡される TxEngine 送信操作の数は、TxEngine で指定された最大数によって制限されます。 この制限は、特定キュー、TxMgr から送信しようとし、TIL で空き容量が増えると、時間の経過と共に変化する可能性があります。

## <a name="host---target-tx-transfer-scheduling"></a>ホストのターゲット TX 転送のスケジュール設定


TxMgr、TxEngine するのにフレームを送信するのに 1 つの送信スレッドを使用します。 バックログ キューがある限り、アクティブにする、TxEngine フレームを送信する送信スレッドがあります。

TxMgr キュー モードに応じて次のようにキューをスケジュールします。

WDI ポートのキュー (**TargetPriorityQueueing**が TRUE に等しい)、バックログされたポートのすべてのキューを介した Deficit ラウンド ロビン (DRR) を使って TxMgr サービスのキュー。

WDI PeerTID キュー (**TargetPriorityQueueing** false)、TxMgr サービス AC の優先順位に従ってキューのすべてのキューを枯渇させてなしとボトルネック TIL 内のリソースに、いずれかにより、ターゲットが RA TID 間で共有されます公正な方法でストリーム。 このようなリソースの過剰の共有を占め低速のストリームができないようにします。

一般に、スケジューラは、特定の時点から送信するのにピア TID キューを選択するのに DRR を使用します。 各キューの場合は、DRR は、各ラウンドでキューから送信するには、8 進数の数を制限するクォンタム パラメーターを関連付けます。 TxEngine では、1 つまたは 2 つの転送の営業案件の予想サイズに合わせて、キューに関連する各送信操作では、このパラメーターを更新します。

一般に、RA TID キューのみ DRR スケジューラ サービスは、最も高い優先順位のバックログの AC に関連付けられています。 枯渇を防ぐためには、スケジューラはすべてのバックログ キューで DRR を定期的に実行します。

### <a name="priority-mapping-for-ihv-reserved-extended-tids"></a>IHV の優先度のマッピングには、拡張 Tid が予約されています。

フレーム、IHV 予約済みの範囲のマップには、次の拡張 TID を IHV によって挿入では、優先順位でスケジューリングの目的で ACs を拡張します。 テーブルでは、優先度の昇順にします。

|              |        |        |        |        |         |         |         |         |
|--------------|--------|--------|--------|--------|---------|---------|---------|---------|
| 拡張 TID | 17     | 18     | 19     | 20     | 21      | 22      | 23      | 24      |
| 拡張 AC  | AC\_BK | AC\_BE | AC\_VI | AC\_VO | AC\_PR0 | AC\_PR1 | AC\_PR2 | AC\_PR3 |

 

WDI ポートのキューのうち、挿入されたすべてのフレームは、拡張 TID に関係なく均等に処理します。

## <a name="txmgr-txengine-interface"></a>TxMgr TxEngine インターフェイス


### <a name="requests-to-txengine"></a>TxEngine への要求

-   [*ミニポート\_WDI\_TX\_中止*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-miniport_wdi_tx_abort)
-   [*ミニポート\_WDI\_TX\_データ\_送信*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-miniport_wdi_tx_data_send)
-   [*ミニポート\_WDI\_TX\_話して\_キュー\_IN\_順序*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-miniport_wdi_tx_tal_queue_in_order)
-   [*ミニポート\_WDI\_TX\_話して\_送信*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-miniport_wdi_tx_tal_send)
-   [*ミニポート\_WDI\_TX\_話して\_送信\_完了*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-miniport_wdi_tx_tal_send_complete)
-   [*ミニポート\_WDI\_TX\_ターゲット\_DESC\_DEINIT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-miniport_wdi_tx_target_desc_deinit)
-   [*ミニポート\_WDI\_TX\_ターゲット\_DESC\_INIT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-miniport_wdi_tx_target_desc_init)

### <a name="indications-from-txengine"></a>TxEngine からインジケーター

-   [*NDIS\_WDI\_TX\_デキュー\_IND*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-ndis_wdi_tx_dequeue_ind)
-   [*NDIS\_WDI\_TX\_転送\_完了\_IND*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-ndis_wdi_tx_transfer_complete_ind)
-   [*NDIS\_WDI\_TX\_送信\_完了\_IND*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-ndis_wdi_tx_send_complete_ind)
-   [*NDIS\_WDI\_TX\_クエリ\_RA\_TID\_状態*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-ndis_wdi_tx_query_ra_tid_state)

### <a name="tx-specific-control-requests"></a>特定のコントロール要求の送信

-   [*ミニポート\_WDI\_TX\_ピア\_バックログ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-miniport_wdi_tx_peer_backlog)

### <a name="tx-specific-control-indications"></a>テキサス州の特定のコントロールがないです。

-   [*NDIS\_WDI\_TX\_送信\_一時停止\_IND*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-ndis_wdi_tx_send_pause_ind)
-   [*NDIS\_WDI\_TX\_SEND\_RESTART\_IND*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-ndis_wdi_tx_send_restart_ind)
-   [*NDIS\_WDI\_TX\_リリース\_フレーム\_IND*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-ndis_wdi_tx_release_frames_ind)
-   [*NDIS\_WDI\_TX\_INJECT\_FRAME\_IND*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-ndis_wdi_tx_inject_frame_ind)

## <a name="related-topics"></a>関連トピック


[WDI TX パス関数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)

[**NET\_バッファー\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_buffer_list)

[**WDI\_TXRX\_機能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/ns-dot11wdi-_wdi_txrx_target_capabilities)

 

 






