---
title: 受信セグメント結合の例
description: このセクションでは、順番に受信され、1 つの遅延プロシージャ呼び出し (DPC) で処理されるセグメントの例を使用して結合アルゴリズムを示しています。
ms.assetid: BC4C3216-683B-4E86-B2DF-F75FFCA7DACC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: abf61775d1421eaf92e4d26954cc00786198881d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385494"
---
# <a name="examples-of-receive-segment-coalescing"></a>受信セグメント結合の例


このセクションでは、順番に受信され、1 つの遅延プロシージャ呼び出し (DPC) で処理されるセグメントの例を使用して結合アルゴリズムを示しています。

このページを使用して X と X' の連続するセグメントをラベル付けします。 他のすべてのセグメントと 1 つのまとめられた単位 (SCU) フィールドは」の説明に従って[TCP/IP セグメントの結合規則](rules-for-coalescing-tcp-ip-packets.md)します。

## <a name="example-1-data-segments"></a>例 1:データ セグメント


### <a name="segment-description"></a>セグメントの説明

同じ TCP 接続に属している 10 個の連続するセグメントが処理されます。 すべての次の条件がそれぞれ該当します。

-   X’.SEQ == X.NXT

-   X'SEQ &gt; X.SEQ

-   X’.ACK == X.ACK

これらのセグメントの [なし] には、例外が生成されます。
### <a name="result"></a>結果

10 個のセグメントから 1 つ SCU が形成されます。 これは、1 つとして示されます[ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376) 1 つの[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388).

## <a name="example-2-data-segments-followed-by-an-exception-followed-by-data-segments"></a>例 2:データ セグメントの後に、例外の後に、データ セグメント


### <a name="segment-description"></a>セグメントの説明

同じ TCP 接続に属する 5 つの連続するセグメントが処理されます。 すべての次の条件がそれぞれ該当します。

-   X’.SEQ == X.NXT

-   X'SEQ &gt; X.SEQ

-   X’.ACK == X.ACK

これらのセグメントの [なし] には、例外が生成されます。
6 番目のセグメントはルール番号 3 のに基づいて例外を生成、TCP SACK オプションで重複した ACK セグメント[TCP/IP セグメントの結合規則](rules-for-coalescing-tcp-ip-packets.md)します。

**注**  ここでは、TCP オプションを処理するための例外ルールは優先され、そのため、結合規則を上書きします。

 

同じ TCP 接続に属する 2 つの連続するセグメントが処理されます。 すべての次の条件がそれぞれ該当します。

-   X’.SEQ == X.NXT

-   X'SEQ &gt; X.SEQ

-   X’.ACK == X.ACK

これらのセグメントの [なし] には、例外が生成されます。
### <a name="result"></a>結果

最初の 5 つのセグメントから 1 つ SCU が形成されます。 6 番目のセグメントには、SCU を形成されていません。

7 番目と 8 番目のセグメントは、まとめて、SCU を形成します。

A [ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388)チェーンが 3 つ示される**NET\_バッファー\_一覧**各構造体1 つを持つ[ **NET\_バッファー**](https://msdn.microsoft.com/library/windows/hardware/ff568376)します。 受信したセグメントの順序は維持されます。

## <a name="example-3-data-segments-followed-by-multiple-window-updates"></a>例 3: 複数のウィンドウの更新後に、データ セグメント


### <a name="segment-description"></a>セグメントの説明

同じ TCP 接続に属する 5 つの連続するセグメントが処理されます。 すべての次の条件がそれぞれ該当します。

-   X’.SEQ == X.NXT

-   X'SEQ &gt; X.SEQ

-   X’.ACK == X.ACK

これらのセグメントの [なし] には、例外が生成されます。
6 番目のセグメントは、純粋の ACK セグメントでウィンドウの更新であります。WND に次のフローチャートで示すように、65535 を = です。

![tcp タイムスタンプ オプションを使用して結合のセグメントの規則を記述するフローチャート](images/rsc-rules2.png)

7 番目のセグメントは、純粋の ACK セグメントでウィンドウの更新であります。WND 同じフローチャートのように、131070 を = です。

### <a name="result"></a>結果

7 セグメントから 1 つ SCU が形成されます。 これは、1 つとして示されます[ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376) 1 つの[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388).

SCU します。WND = 131070、この値に基づいて、チェックサムを更新します。

## <a name="example-4-piggybacked-acks-mixed-with-data-segments"></a>例 4:データ セグメントで追加された Ack の混在


### <a name="segment-description"></a>セグメントの説明

同じ TCP 接続に属する 3 つの連続するセグメントが処理されます。 すべての次の条件がそれぞれ該当します。

-   X’.SEQ == X.NXT

-   X'SEQ &gt; X.SEQ

-   X’.ACK == X.ACK

これらのセグメントの [なし] には、例外が生成されます。
同じ TCP 接続に属する 2 つの連続するセグメントが処理されます。 すべての次の条件がそれぞれ該当します。

-   X’.SEQ == X.NXT

-   X'SEQ &gt; X.SEQ

-   X’.ACK == X.ACK

これらのセグメントの [なし] には、例外が生成されます。
### <a name="result"></a>結果

5 つのセグメントから 1 つ SCU が形成されます。 これは、1 つとして示されます[ **NET\_バッファー** ](https://msdn.microsoft.com/library/windows/hardware/ff568376) 1 つの[ **NET\_バッファー\_一覧**](https://msdn.microsoft.com/library/windows/hardware/ff568388). SCU します。確認は、最後の SEG.ACK で設定されます。

 

 





