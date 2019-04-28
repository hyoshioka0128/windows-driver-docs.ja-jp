---
title: Receive Segment Coalescing の概要
description: データを受信するときに、ミニポート ドライバー、NDIS、および TCP/IP する必要がありますすべてを見て各セグメントのヘッダー情報とは別にします。
ms.assetid: 1E9BC335-BB62-415B-B242-D63672A4E406
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ade849ed2c05e014f0b8c9ca380c7efbeecd520
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365741"
---
# <a name="overview-of-receive-segment-coalescing"></a>Receive Segment Coalescing の概要


データを受信するときに、ミニポート ドライバー、NDIS、および TCP/IP する必要がありますすべてを見て各セグメントのヘッダー情報とは別にします。 大量のデータを受信しているときに、大量のオーバーヘッドが作成されます。 結合 (RSC) では、このオーバーヘッドを削減 NDIS および TCP/IP は必要なシーケンス全体の 1 つのヘッダーにのみ表示されるように、ホストの TCP/IP にスタックの 1 つの操作で受信したセグメントを渡してのシーケンスを結合してセグメントを受信します。

RSC は方法で結合をサポートするためのものです。

-   TCP の輻輳やフロー制御のメカニズムの通常の動作に干渉しません。

-   TCP スタックで使用される情報を破棄しないパケットに連結します。

ネットワーク カードの RSC 対応のミニポート ドライバーが必要です。

-   セグメントを結合するときに、標準的な一連のルールに従ってください。

-   ホストの TCP/IP スタックを特定の帯域外の情報を提供します。

次のセクションでは、RSC の概要を示します。

-   [TCP/IP セグメントの結合規則](rules-for-coalescing-tcp-ip-packets.md)
-   [まとめられたセグメントの IP ヘッダーを更新しています](updating-the-ip-headers-for-coalesced-segments.md)
-   [受信の例では、結合セグメント化します。](examples-of-receive-segment-coalescing.md)
-   [セグメントを結合することを示す](indicating-coalesced-segments.md)
-   [例外条件の結合を終了します。](exception-conditions-that-terminate-coalescing.md)

 

 





