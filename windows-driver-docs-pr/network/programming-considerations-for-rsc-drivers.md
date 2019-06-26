---
title: RSC ドライバーのプログラミングに関する考慮事項
description: 次のセクションでは、説明、受信セグメント合体 (RSC) を実装するときに考慮すべき問題の対応のミニポート ドライバー。
ms.assetid: 03FDD557-3918-408A-BD79-64CD52BDD43A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf825aaa588d314792ec620486d50f12c2d73d0e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385465"
---
# <a name="programming-considerations-for-rsc-drivers"></a>RSC ドライバーのプログラミングに関する考慮事項


次のセクションでは、説明、受信セグメント合体 (RSC) を実装するときに考慮すべき問題の対応のミニポート ドライバー。

-   [RSC の統計情報のクエリに応答してください。](#responding-to-queries-for-rsc-statistics)
-   [転送された TCP パケット](#forwarded-tcp-packets)
-   [軽量のフィルターと MUX 中間ドライバーの RSC のサポート](#rsc-support-for-lightweight-filters-and-mux-intermediate-drivers)
-   [Windows フィルタ リング プラットフォーム (WFP) の検査とコールアウト ドライバー](#windows-filtering-platform-wfp-inspection-and-callout-drivers)

## <a name="responding-to-queries-for-rsc-statistics"></a>RSC の統計情報のクエリに応答してください。


NDIS、上にあるドライバー、およびユーザー モード アプリケーションを使用して、 [OID\_TCP\_RSC\_統計](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-rsc-statistics)ミニポート アダプターの RSC の統計情報を取得する OID。 RSC 対応のミニポート ドライバーでは、この OID をサポートする必要があります。

## <a name="forwarded-tcp-packets"></a>転送された TCP パケット


ミニポート ドライバーでは、ホストのためのものではありませんが、別のインターフェイス上に転送されている TCP パケットのセグメントの RSC を実行しないでください。

ホストの TCP/IP スタックは、転送を有効になっているインターフェイスの RSC を無効になります。 弱いホストの転送では、RSC は影響しません。

## <a name="rsc-support-for-lightweight-filters-and-mux-intermediate-drivers"></a>軽量のフィルターと MUX 中間ドライバーの RSC のサポート


リンクの最大転送単位 (MTU) よりも大きいパケットの受信をすべての NDIS 6.30 ライトウェイト フィルター ドライバーをサポートする必要があります。 セグメントのサイズの制限の詳細については、次を参照してください。[を示す 1 つにまとめセグメント](indicating-coalesced-segments.md)します。

NDIS はライトウェイト フィルター ドライバーやホスト スタックに MUX 中間ドライバーは、NDIS 6.20 が動作する場合、インターフェイスの RSC を無効にするか、減らしています。

インターフェイスの NDIS バージョンが 6.30 以降の場合でも、MUX 中間ドライバーは、インターフェイスの RSC を無効にできます。

## <a name="windows-filtering-platform-wfp-inspection-and-callout-drivers"></a>Windows フィルタ リング プラットフォーム (WFP) の検査とコールアウト ドライバー


WFP コールアウト ドライバーは、カスタム引き出し関数を 1 つ以上のカーネル モードのフィルター処理レイヤーで、フィルター エンジンに追加することで、追加のフィルター処理機能を提供します。 コールアウト詳細な検査とパケットのサポートだけでなく変更をストリーミングします。

WFP コールアウト ドライバーのサポートが MTU のリンクよりも大きいパケットを受信して処理のサポート。 (パケット サイズの制限の詳細については、次を参照してください[追跡とを示す 1 つにまとめセグメント](https://docs.microsoft.com/windows-hardware/drivers/network/indicating-coalesced-segments)。)。このような WFP コールアウト ドライバーは、次の操作を行います。

-   大きなパケットを処理するために、登録時にオプトインします。

-   リファレンス ページで指定されているコールアウト ドライバーのフラグを設定、 [ **FWPS\_CALLOUT2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/ns-fwpsk-fwps_callout2_)構造体。

登録されていない大量のパケットを処理するためにオプトインするコールアウト ドライバーたびに WFP は、登録のコンテキストで TCP/IP を通知します。 この通知の処理の一環として、TCP/IP は、インターフェイスの RSC を無効になります。

引き出し線の登録時にアクティブな TCP トラフィックがある場合、TCP/IP は WFP を通知します。 WFP では、RSC が無効になるまでに登録されているフィルターを呼び出す遅延が生じます。 これは、大きなパケットからコールアウト ドライバーを保護します。

 

 





