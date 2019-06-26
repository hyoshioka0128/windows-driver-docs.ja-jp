---
title: レイヤー 2 フィルターの使用
description: レイヤー 2 フィルターの使用
ms.assetid: 679E6DE2-4EFB-44F6-936D-2BF611BC9726
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dee558719fb76a1a1572b1b6ab021bd011e99d1f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371814"
---
# <a name="using-layer-2-filtering"></a>レイヤー 2 フィルターの使用

Windows 8 および Windows の以降のバージョンでは、レイヤー 2 のフィルタ リングがサポートされています。

この WFP 機能は、レイヤー 2 MAC ヘッダーのフィールドのフィルター処理を使用できます。 これらの層は、すべてのパケットを送信または受信ホスト マシンでのパケット単位ごとに呼び出されます。 レイヤーは、送信パス上のパケットの断片化の前後に受信パス上のパケットの再構築する前に呼び出されます。 これらの層は、NDIS ドライバー ライトウェイト フィルター (LWF) からアクセスされます。

> [!NOTE]
> コールアウトは、既にがあるない対応するフィルターをその層の場合、層でパケットをインジェクションできません必要があります。 挿入、 [NET\_バッファー\_一覧](net-buffer-list-structure.md)インジェクションは、対応するレイヤーで、フィルターが存在する場合にのみ実行できるように構造がフィルターの追加と削除と連携する必要があります。 さらに、プロバイダーでは、その他のプロバイダーに属しているフィルターは削除しないでください。 

ここでは、次のトピックについて説明します。

-   [挿入することの MAC フレーム](#injecting-mac-frames)
-   [チェーンのネットワーク バッファーのリストの分類](#classifying-chained-network-buffer-lists)
-   [WFP レイヤー 2 のレイヤーとフィールド](#wfp-layer-2-layers-and-fields)

## <a name="injecting-mac-frames"></a>挿入することの MAC フレーム

コールバックのドライバーは呼び出し、 [ **FwpsInjectMacReceiveAsync0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsinjectmacreceiveasync0)関数が取得から、またはレイヤー 2 の受信データ パスに吸収以前 MAC フレーム (または、フレームの複製) を再挿入するには受信データ パスで、作成された MAC フレームを挿入します。

コールバックのドライバーは呼び出し、 [ **FwpsInjectMacSendAsync0** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsinjectmacsendasync0)関数が取得から、またはレイヤー 2 の送信データ パスに吸収以前 MAC フレーム (または、フレームの複製) を再挿入するには送信データ パスで、作成された MAC フレームを挿入します。

*NetBufferLists*パラメーターを指定できます、 [NET\_バッファー\_一覧](net-buffer-list-structure.md)チェーン。 ただし完了関数呼び出すことができる何度も各セグメントの完了 (NET の 1 つの\_バッファー\_一覧) のチェーン。

最初に分類される同じフィルターに一致した場合は、挿入されたフレームをもう一度分類取得でした。 このため、IP レイヤーに引き出しと同様レイヤー 2 のコールアウトする必要がありますも保護が無限のパケット検査を呼び出して[ **FwpsQueryPacketInjectionState0**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsquerypacketinjectionstate0)します。

また、層に追加することで、吹き出しが必要です。 それ以外の場合、挿入された[NET\_バッファー\_一覧](net-buffer-list-structure.md)完了関数、および NET には完了しません\_バッファー\_一覧は、スタックに進みます。 この場合、動作は未定義、NDIS が挿入された NET を渡そうとすると、ため\_バッファー\_スタック内の次のコンポーネントを一覧します。

[NET\_バッファー\_一覧](net-buffer-list-structure.md)**状態**メンバーにはスタック インジェクションの状態を結果が含まれています。 スタックの挿入の状態の結果は、スタックは、NET に格納された状態\_バッファー\_WFP インジェクション関数が返された後一覧**状態\_成功**します。 使用する必要があります、 **NT\_成功**スタック インジェクションの状態を確認するマクロ、**状態**メンバー。 場合、**状態**値は**状態\_成功**、詳細情報はありません、挿入が成功しました。 **ステータス**メンバーの値を超える**状態\_成功**という意味では、挿入が成功しましたが、考慮すべきインジェクションの詳細がある可能性があります。 **ステータス**はメンバーの値より小さい**状態\_成功**で指定されたため、挿入が失敗した平均値、**状態**メンバー。

## <a name="classifying-chained-network-buffer-lists"></a>チェーンのネットワーク バッファーのリストの分類

既定では、コールアウト ドライバーのみを分類できますネットワーク バッファーのリストに個別にします。 ただし、コールアウト ドライバーを分類できます[NET\_バッファー\_一覧](net-buffer-list-structure.md)場合は、次の両方にパフォーマンスの向上のため、チェーンします。

-   指定します、 **FWP\_コールアウト\_フラグ\_許可\_L2\_バッチ\_分類**フラグ、**フラグ**のメンバー[ **FWPS\_CALLOUT2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ns-fwpsk-fwps_callout2_)構造体。
-   登録、 [ *classifyFn2* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nc-fwpsk-fwps_callout_classify_fn2)を分類できます関数[NET\_バッファー\_一覧](net-buffer-list-structure.md)チェーン。

> [!WARNING]
> ただし、コールアウト ドライバーでは設定した場合、 **FWP_CALLOUT_FLAG_ALLOW_L2_BATCH_CLASSIFY**フラグ、NET_BUFFER_LISTs を変更する、次の関数は使用できません。
> 
> - [FwpsReferenceNetBufferList0](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsreferencenetbufferlist0)
> - [FwpsDereferenceNetBufferList0](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsdereferencenetbufferlist0)
> - [FwpsAllocateCloneNetBufferList0](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsallocateclonenetbufferlist0)
> - [FwpsFreeCloneNetBufferList0](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nf-fwpsk-fwpsfreeclonenetbufferlist0)
>
> このフラグを設定して**FwpsAllocateCloneNetBufferList0**は常に返します、 **INVALID_PARAMETER**エラー。 サード生じる予期せず失敗 NET の参照カウントを管理するパーティ コールアウト ドライバー\_バッファー\_リスト、原因が送信および受信を停止する操作。

## <a name="wfp-layer-2-layers-and-fields"></a>WFP レイヤー 2 のレイヤーとフィールド

仮想スイッチがフィルター処理するためのランタイム フィルタ リング層識別子は次のとおりです。

**FWPS\_レイヤー\_受信\_MAC\_フレーム\_イーサネット**

**FWPS\_レイヤー\_送信\_MAC\_フレーム\_イーサネット**

**FWPS\_レイヤー\_受信\_MAC\_フレーム\_ネイティブ**

**FWPS\_レイヤー\_送信\_MAC\_フレーム\_ネイティブ**

仮想スイッチがフィルター処理するためのデータ フィールドの識別子は次のとおりです。

[**FWPS\_フィールド\_受信\_MAC\_フレーム\_イーサネット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ne-fwpsk-fwps_fields_inbound_mac_frame_ethernet_)

[**FWPS\_フィールド\_送信\_MAC\_フレーム\_イーサネット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ne-fwpsk-fwps_fields_outbound_mac_frame_ethernet_)

[**FWPS\_フィールド\_受信\_MAC\_フレーム\_ネイティブ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ne-fwpsk-fwps_fields_inbound_mac_frame_native_)

[**FWPS\_フィールド\_送信\_MAC\_フレーム\_ネイティブ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ne-fwpsk-fwps_fields_outbound_mac_frame_native_)

 

 





