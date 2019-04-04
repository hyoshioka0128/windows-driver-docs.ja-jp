---
title: MapTransferEx ルーチンを使用してください。
description: MapTransferEx ルーチンでは、以前に割り当てられた DMA リソースのセットを初期化し、DMA の転送を開始します。
ms.assetid: 79D3DDB2-B134-43B2-A6CC-94035C793047
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c72ea9dd940cee71186c0b829bc536cf74143aed
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549245"
---
# <a name="using-the-maptransferex-routine"></a>MapTransferEx ルーチンを使用してください。


[ **MapTransferEx** ](https://msdn.microsoft.com/library/windows/hardware/hh406521)ルーチンは、DMA の以前に割り当てられたリソースのセットを初期化し、DMA の転送を開始します。 このルーチンは、バージョン 3 の DMA 操作インターフェイスで使用できます。 このインターフェイスのバージョン 3 は、Windows 8 以降ではサポートされています。 DMA 操作のインターフェイスの詳細については、[ **DMA\_操作**](https://msdn.microsoft.com/library/windows/hardware/ff544071)を参照してください。

## <a name="comparison-of-maptransferex-to-maptransfer"></a>MapTransfer に MapTransferEx の比較


**MapTransferEx**の改善されたバージョン、 [ **MapTransfer** ](https://msdn.microsoft.com/library/windows/hardware/ff554402)ルーチン。 **MapTransfer**は DMA 操作インターフェイス、Windows 2000 では、バージョン 1 以降のすべてのバージョンで使用できます。 1 回の呼び出しに**MapTransfer** MDL から物理メモリの 1 つの連続したブロックをマップすることができます。 ただし、複雑な DMA 転送用のデータ バッファーの説明は、MDL チェーンによって、チェーン内の各 MDL が物理的に連続するメモリのいくつかのブロックを表す場合があります。 使用する**MapTransfer**ドライバーにそのようなバッファーを転送するには、多くの呼び出しを行う必要があります**MapTransfer**します。 通常、これらの呼び出しは入れ子になったループのペア内で行われます。 各 MDL では、[次へ] を 1 つの連続した物理メモリのブロックから内側のループが反復処理し、MDL チェーン内の次に 1 つの MDL から外側のループが反復処理します。

これに対し、1 つ呼び出し**MapTransferEx** DMA の複雑な転送全体のデータ バッファーを転送することができます。 次の 3 つ**MapTransferEx**パラメーターが転送に使用するバッファー メモリについて説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>パラメーター</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><em>Mdl</em></td>
<td><p>1 つまたは複数の MDLs のチェーン内の最初の MDL へのポインター。 MDL チェーンの詳細については、<a href="using-mdls.md" data-raw-source="[Using MDLs](using-mdls.md)">を使用して MDLs</a>を参照してください。</p></td>
</tr>
<tr class="even">
<td><em>オフセット</em></td>
<td><p>MDL チェーンによって説明されているメモリの開始位置からバッファーのバイト オフセット。</p></td>
</tr>
<tr class="odd">
<td><em>長さ</em></td>
<td><p>データ バッファーの長さ、(バイト単位) を格納している場所へのポインター。</p></td>
</tr>
</tbody>
</table>

 

開始時、 **MapTransferEx**を呼び出すには、 **MapTransferEx**ルーチンが MDL チェーンを検索して、バッファーの先頭を進めます。 バッファーの先頭が指定された、*オフセット*パラメーター。 次に、最後に、バッファーの先頭から作業、 **MapTransferEx**スキャッター/ギャザー一覧が各バッファー フラグメントの一覧では、物理的に連続する MDL チェーンからメモリ ブロックを構築します。 この一覧を構築する**MapTransferEx** MDL チェーン内の次に、各 MDL 内で次にメモリの 1 つの物理的に連続するブロックと 1 つの MDL からの手順。 スキャッター/ギャザーの一覧で説明されているバッファー メモリの総量がで指定したバイト数と等しい場合に、リストの構築が完了したら、 \**長さ*入力パラメーター。 結果のスキャッター/ギャザー リストでバッファー フラグメントの順序は、MDL チェーン内の物理的に連続するブロックの順序と一致します。

## <a name="multiple-calls-to-maptransferex"></a>MapTransferEx を複数回呼び出す


**MapTransferEx**常にできないことがあります全体の DMA データ バッファーに 1 回の呼び出しを転送します。 必要となる条件の一部を次に示します**MapTransferEx**転送の完了には複数回呼び出されます。

-   DMA アダプターには、マップのレジスタが必要ですし、アダプターに割り当てられているマップのレジスタの数がバッファー全体を記述するのに十分でないです。
-   スキャッター/ギャザーの一覧を格納するドライバーによって割り当てられたストレージは、バッファー全体のスキャッター/ギャザーのリストを格納するのに十分な大きさが。
-   転送では、ハードウェアのスキャッター/ギャザー リストで指定できるバッファー フラグメントの数を制限するシステム DMA コント ローラーを使用します。

このような場合は、のすべての**MapTransferEx** 1 回の呼び出しで可能な限り多くのデータ バッファーをマップし、呼び出しによってマップされたバッファーの量をドライバーに指示します。 上記の一覧には、複数の呼び出しが必要となるプラットフォームに固有のキャッシュ動作など、他の条件が含まれていません**MapTransferEx**転送を完了します。 将来のハードウェア プラットフォームには、DMA 転送の長さに追加の制約を課すことがあります。 これらの理由から、ドライバー開発者向けがケースにも適切に処理するには、そのドライバーを設計する必要があります**MapTransferEx** 1 回の呼び出しで、全体の DMA データ バッファーをマップすることはできません。

呼び出しの前に**MapTransferEx**、呼び出し元のセット、 \**長さ*パラメーターをマップする必要がある DMA データ バッファー内のバイト数。 、戻る前に**MapTransferEx**設定\**長さ*の呼び出しによって実際にマップされているバッファー内のバイト数。 ときに、 **MapTransferEx**呼び出しで指定したとおり、全体のバッファーの長さをマップできません、 \**長さ*の出力値は、入力値\**長さ*がその入力値より小さい。 DMA 転送は、2 つ以上が必要な場合**MapTransferEx**呼び出し、呼び出し元のドライバーを入手する必要があります、 \**長さ*指定できる前に 1 回の呼び出しから値を出力する、 \* *長さ*次の呼び出しの値を入力します。

たとえば場合、 **MapTransferEx**呼び出しは X のみを転送できますバイトをバッファーとの間*オフセット*= B と\**長さ*= N (入力) に次に返された場合に、\**長さ*X を = です。次回の呼び出しの**MapTransferEx**、ドライバーを設定する必要があります*オフセット*= B + X と\**長さ*= N - X。両方の呼び出しで同じ MDL チェーンは変更せずに使用します。

呼び出し元が指定されている場合、 [ *DmaCompletionRoutine*](https://msdn.microsoft.com/library/windows/hardware/hh450991)、 **MapTransferEx**書き込みます、 \**長さ*前に、の値を出力スケジュール、 *DmaCompletionRoutine*を実行します。 この動作により、更新された\**長さ*値が使用する前に常に、 *DmaCompletionRoutine*を実行します。 たとえば、DMA 転送では、2 つが必要な場合**MapTransferEx**呼び出し、 *DmaCompletionRoutine*呼び出しの最初のスケジュールを取得できることを\**長さ*最初の呼び出しから値を出力します。 ルーチンを計算するこの値を使用できますし、 \**長さ*2 つ目の呼び出しの値を入力します。 通常、*長さ*パラメーター内の場所をポイントする、 \* *CompletionContext*に用意されている値、 *DmaCompletionRoutine*として、パラメーター。

 

 




