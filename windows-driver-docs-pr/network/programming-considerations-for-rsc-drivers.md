---
title: RSC ドライバーのプログラミングに関する考慮事項
description: 次のセクションでは、受信セグメント合体 (RSC) 対応のミニポートドライバーを実装する際に考慮する必要がある問題について説明します。
ms.assetid: 03FDD557-3918-408A-BD79-64CD52BDD43A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6aab90a36edfaf6173db8d4785b1c2e8068a8a0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843477"
---
# <a name="programming-considerations-for-rsc-drivers"></a>RSC ドライバーのプログラミングに関する考慮事項


次のセクションでは、受信セグメント合体 (RSC) 対応のミニポートドライバーを実装する際に考慮する必要がある問題について説明します。

-   [RSC 統計に対するクエリへの応答](#responding-to-queries-for-rsc-statistics)
-   [転送された TCP パケット数](#forwarded-tcp-packets)
-   [ライトウェイトフィルターと MUX 中間ドライバーの RSC サポート](#rsc-support-for-lightweight-filters-and-mux-intermediate-drivers)
-   [Windows フィルタリングプラットフォーム (WFP) 検査およびコールアウトドライバー](#windows-filtering-platform-wfp-inspection-and-callout-drivers)

## <a name="responding-to-queries-for-rsc-statistics"></a>RSC 統計に対するクエリへの応答


NDIS、それ以降のドライバー、およびユーザーモードアプリケーションでは、 [oid\_TCP\_rsc\_STATISTICS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-tcp-rsc-statistics) oid を使用して、ミニポートアダプターの rsc 統計を取得します。 RSC 対応ミニポートドライバーは、この OID をサポートする必要があります。

## <a name="forwarded-tcp-packets"></a>転送された TCP パケット数


ミニポートドライバーは、ホスト用ではなく、別のインターフェイスで転送される TCP パケット内のセグメントに対して RSC を実行しないでください。

ホストの TCP/IP スタックは、転送が有効になっているすべてのインターフェイスで RSC を無効にします。 ホストの弱い転送は RSC には影響しません。

## <a name="rsc-support-for-lightweight-filters-and-mux-intermediate-drivers"></a>ライトウェイトフィルターと MUX 中間ドライバーの RSC サポート


すべての NDIS 6.30 ライトウェイトフィルタードライバーは、リンク最大転送単位 (MTU) を超える受信パケットをサポートする必要があります。 セグメントサイズの制限の詳細については、「[結合セグメントを示す](indicating-coalesced-segments.md)」を参照してください。

ホストスタック内のライトウェイトフィルタードライバーまたは MUX 中間ドライバーが NDIS 6.20 以下の場合、NDIS はインターフェイスで RSC を無効にします。

MUX 中間ドライバーは、インターフェイスの NDIS バージョンが6.30 以上の場合でも、インターフェイスで RSC を無効にすることができます。

## <a name="windows-filtering-platform-wfp-inspection-and-callout-drivers"></a>Windows フィルタリングプラットフォーム (WFP) 検査およびコールアウトドライバー


WFP コールアウトドライバーは、1つまたは複数のカーネルモードフィルターレイヤーのフィルターエンジンにカスタムコールアウト関数を追加することにより、追加のフィルター機能を提供します。 コールアウトでは、詳細な検査とパケット、およびストリームの変更がサポートされています。

WFP コールアウトドライバーは、リンク MTU を超えるサポートの受信パケットをサポートする場合があります。 (パケットサイズの制限の詳細については、「結合された[セグメントの追跡と指示](https://docs.microsoft.com/windows-hardware/drivers/network/indicating-coalesced-segments)」を参照してください)。このような WFP コールアウトドライバーでは、次の操作を行う必要があります。

-   大規模なパケットを処理するために登録中にオプトインします。

-   [**Fwps\_CALLOUT2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_callout2_)構造体の参照ページで指定されているように、コールアウトドライバーフラグを設定します。

サイズの大きいパケットを処理するように選択されていないコールアウトドライバーが登録されている場合、WFP は、登録のコンテキストで TCP/IP に通知します。 この通知の処理の一環として、TCP/IP はインターフェイスで RSC を無効にします。

コールアウト登録中にアクティブな TCP トラフィックがある場合、TCP/IP は WFP に通知します。 RSC が無効になるまで、登録済みフィルターの呼び出しが遅延されます。 これにより、サイズの大きいパケットからコールアウトドライバーが保護されます。

 

 





