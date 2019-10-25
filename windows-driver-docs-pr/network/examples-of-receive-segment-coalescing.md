---
title: 受信セグメント結合の例
description: このセクションでは、1つの遅延プロシージャ呼び出し (DPC) で注文および処理されるセグメントの例を使用して、結合アルゴリズムについて説明します。
ms.assetid: BC4C3216-683B-4E86-B2DF-F75FFCA7DACC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b953da7fd4c14447be22a63df76ff4ea3996d61b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834753"
---
# <a name="examples-of-receive-segment-coalescing"></a>受信セグメント結合の例


このセクションでは、1つの遅延プロシージャ呼び出し (DPC) で注文および処理されるセグメントの例を使用して、結合アルゴリズムについて説明します。

このページでは、連続するセグメントのラベル付けに X と X を使用します。 他のすべてのセグメントと1つの結合単位 (SCU) フィールドは、「 [Tcp/ip セグメントを結合するための規則](rules-for-coalescing-tcp-ip-packets.md)」で説明されています。

## <a name="example-1-data-segments"></a>例 1: データセグメント


### <a name="segment-description"></a>セグメントの説明

同じ TCP 接続に属する10個の連続するセグメントが処理されます。 次のすべての条件が該当します。

-   X '。SEQ = = X. NXT

-   X'SEQ &gt; X. SEQ

-   X '。ACK = = X。 ACK

これらのセグメントのいずれも例外を生成しません。
### <a name="result"></a>結果

1つの SCU は10個のセグメントから形成されます。 これは、単一の[**net\_バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)に1つの[**net\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)として示されます。

## <a name="example-2-data-segments-followed-by-an-exception-followed-by-data-segments"></a>例 2: データセグメントの後に例外が続き、その後にデータセグメントが続く


### <a name="segment-description"></a>セグメントの説明

5同じ TCP 接続に属する連続するセグメントが処理されます。 次のすべての条件が該当します。

-   X '。SEQ = = X. NXT

-   X'SEQ &gt; X. SEQ

-   X '。ACK = = X。 ACK

これらのセグメントのいずれも例外を生成しません。
6番目のセグメントは、TCP SACK オプションを使用した重複する ACK セグメントで、 [Tcp/ip セグメントを結合するルール](rules-for-coalescing-tcp-ip-packets.md)のルール番号3に基づいて例外を生成します。

この**場合  TCP**オプションを処理する例外規則が優先されるため、合体規則がオーバーライドされます。

 

2同じ TCP 接続に属する連続するセグメントが処理されます。 次のすべての条件が該当します。

-   X '。SEQ = = X. NXT

-   X'SEQ &gt; X. SEQ

-   X '。ACK = = X。 ACK

これらのセグメントのいずれも例外を生成しません。
### <a name="result"></a>結果

1つの SCU は、最初の5つのセグメントから形成されます。 6番目のセグメントは SCU を形成しません。

7番目と8番目のセグメントでは、SCU が一緒に形成されます。

Net [ **\_バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)チェーンは、それぞれ1つの[**net\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)を持つ3つの**net\_バッファー\_リスト**構造で示されます。 受信したセグメントの順序は維持されます。

## <a name="example-3-data-segments-followed-by-multiple-window-updates"></a>例 3: データセグメント、その後に複数のウィンドウを更新する


### <a name="segment-description"></a>セグメントの説明

5同じ TCP 接続に属する連続するセグメントが処理されます。 次のすべての条件が該当します。

-   X '。SEQ = = X. NXT

-   X'SEQ &gt; X. SEQ

-   X '。ACK = = X。 ACK

これらのセグメントのいずれも例外を生成しません。
6番目のセグメントは、SEG を使用したウィンドウ更新である純粋な ACK です。次のフローチャートに示すように、WND = 65535。

![tcp タイムスタンプオプションを使用してセグメントを結合するための規則を説明するフローチャート](images/rsc-rules2.png)

7番目のセグメントは、SEG を使用したウィンドウ更新である純粋な ACK です。WND = 131070 同じフローチャートに示されています。

### <a name="result"></a>結果

1つの SCU は7個のセグメントから形成されています。 これは、単一の[**net\_バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)に1つの[**net\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)として示されます。

SCU。WND = 131070、チェックサムはこの値に基づいて更新されます。

## <a name="example-4-piggybacked-acks-mixed-with-data-segments"></a>例 4: データセグメントと共に上乗せされる Ack


### <a name="segment-description"></a>セグメントの説明

3同じ TCP 接続に属する連続するセグメントが処理されます。 次のすべての条件が該当します。

-   X '。SEQ = = X. NXT

-   X'SEQ &gt; X. SEQ

-   X '。ACK = = X。 ACK

これらのセグメントのいずれも例外を生成しません。
2同じ TCP 接続に属する連続するセグメントが処理されます。 次のすべての条件が該当します。

-   X '。SEQ = = X. NXT

-   X'SEQ &gt; X. SEQ

-   X '。ACK = = X。 ACK

これらのセグメントのいずれも例外を生成しません。
### <a name="result"></a>結果

1つの SCU は5つのセグメントから形成されます。 これは、単一の[**net\_バッファー\_リスト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list)に1つの[**net\_バッファー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer)として示されます。 SCU。ACK は最後のセグメントに設定されます。

 

 





