---
title: ログを使用した重要イベントの追跡
description: ログを使用した重要イベントの追跡
ms.assetid: 297336c2-85fb-4235-a7ab-0bbf571b8b98
keywords:
- カーネル デバッグ ストリーム、ビデオ ストリーム失速、ログ記録
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc8b7ee79e43c7e50043218a41f278cc51753eb2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376362"
---
# <a name="using-logging-to-track-important-events"></a>ログを使用した重要イベントの追跡


一般に、データは、イベント、ミニドライバーの処理、およびバッファーの入力候補をトリガーすることによってのみ下流移動されます。 ハングの原因を特定または停止します。

- 確認が一致しない**KsGate * Xxx*** 呼び出し。

- 省略すると確認**Ks*Xxx*AttemptProcessing**呼び出し。

- 外観に関連するなど、イベントをトリガーするコードの問題をコードか、参照、問題のストリームの暗証番号 (pin) フラグまたはを呼び出す**KsPinAttemptProcessing**します。

- 関連する処理のディスパッチ、具体的にはハードウェアに、キューに登録および複製ポインターが作成されたコードで問題を探します。

- 特に、バッファーが完了するか、呼び出しが、問題に関連するドライバーのコードで遅延プロシージャ呼び出し (DPC) を探して[KsStreamPointerDelete](https://go.microsoft.com/fwlink/p/?linkid=56550)します。

- ストリームのスタートアップ コードで問題を探します。

(複製とハードウェアのプログラミング) などのバッファーの取得を処理するなど、影響を受けたリージョン内のすべてをログに記録する情報を収集する最も効果的な方法は、バッファー (クローンの削除) などのリリースと、ゲート操作。 この情報のほとんどは、高タイミングに応じて変わりますがおり、メモリ ベースのログまたは ETW が必要です。

ローリング メモリ ベースのログを維持するには、次のコードを使用します。

```cpp
typedef struct _LOGENTRY {
    ULONG Tag;
    ULONG Arg[3];
} LOGENTRY, *PLOGENTRY;
#define LOGSIZE 2048
LONG g_LogCount;
LOGENTRY g_Log [LOGSIZE];
#define LOG(tag,arg1,arg2,arg3) do { \
    LONG i = InterlockedIncrement (&g_LogCount) % LOGSIZE; \
    g_Log [i].Tag = tag; \
    g_Log [i].Arg [0] = (ULONG)(arg1); \
    g_Log [i].Arg [1] = (ULONG)(arg2); \
    g_Log [i].Arg [2] = (ULONG)(arg3); \
} while (0)
```dbgcmd

Then, use a simple "dc g\_Log" to view the contents of the **g\_Log** array in the debugger.

The following example uses the above memory-based scheme to determine the cause of a processing stall. Output is from an AVStream streaming scenario in graphedt. The following minidriver events were logged:

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Abbreviation</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>Strt</em></p></td>
<td align="left"><p>This event occurs when the minidriver first queues buffers for the device from within the minidriver's <em>Start</em> dispatch.</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>Prc&lt;</em></p></td>
<td align="left"><p>This event occurs at the start of the minidriver's <em>Process</em> dispatch.</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>AddB</em></p></td>
<td align="left"><p>This event occurs when the minidriver queues buffers to the device from within its <em>Process</em> dispatch.</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>DPC&lt;</em></p></td>
<td align="left"><p>This event occurs at the start of the minidriver's <em>CallOnDPC</em>. It indicates buffer completion.</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>Atmp</em></p></td>
<td align="left"><p>This event occurs when the minidriver calls from within the DPC to <strong>KsPinAttemptProcessing</strong>.</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>Dele</em></p></td>
<td align="left"><p>This event occurs when the minidriver calls from within the DPC to delete a clone stream pointer.</p></td>
</tr>
</tbody>
</table>

 

Log excerpts are as follows:

```text
f9494b80  3c435044 816e2c90 00000000 00000000  DPC<.,n.........
f9494b90  656c6544 816e2c90 81750260 00000000  Dele.,n.`.u.....
f9494ba0  706d7441 816e2c90 ffa4d418 00000000  Atmp.,n.........
f9494bb0  3c637250 819c1f00 00000000 00000000  Prc<............
f9494bc0  42646441 819c1f00 ffa2eb08 00000000  AddB............
f9494bd0  3c435044 816e2c90 00000000 00000000  DPC<.,n.........
f9494be0  656c6544 816e2c90 ffa80348 00000000  Dele.,n.H.......
f9494bf0  706d7441 816e2c90 ffa4d418 00000000  Atmp.,n.........
f9494c00  3c637250 819c1f00 00000000 00000000  Prc<............
f9494c10  42646441 819c1f00 ffa3d9b8 00000000  AddB............
```

この最初のログの抜粋は、ストリーミングの通常の状態の代表です。 最初の行で、ミニドライバーの*CallOnDPC*バッファーを完了すると呼びます (*DPC&lt;* )。 バッファーを削除 (*Dele*)、および**KsPinAttemptProcessing**はリーディング エッジを移動すると呼ばれるキューのすべての未処理のバッファーがある場合 (*Atmp*)。 この場合が、プロセスのディスパッチへの呼び出しから見たことができます (*Prc&lt;* )。 バッファーの詳細については、キューに追加されます (*AddB*)、およびシナリオ全体が繰り返されます。

この次の抜粋には、停止が発生する前に、適切なログの最後のエントリが含まれます。

```text
f949b430  3c435044 816e2c90 00000000 00000000  DPC<.,n.........
f949b440  656c6544 816e2c90 ffac4de8 00000000  Dele.,n..M......
f949b450  706d7441 816e2c90 ffa4d418 00000000  Atmp.,n.........
f949b460  3c435044 816e2c90 00000000 00000000  DPC<.,n.........
f949b470  656c6544 816e2c90 816ffc80 00000000  Dele.,n...o.....
f949b480  706d7441 816e2c90 ffa4d418 00000000  Atmp.,n.........
f949b490  3c435044 816e2c90 00000000 00000000  DPC<.,n.........
f949b4a0  656c6544 816e2c90 ffa80348 00000000  Dele.,n.H.......
f949b4b0  706d7441 816e2c90 ffa4d418 00000000  Atmp.,n.........
f949b4c0  3c435044 816e2c90 00000000 00000000  DPC<.,n.........
f949b4d0  656c6544 816e2c90 8174e1c0 00000000  Dele.,n...t.....
f949b4e0  706d7441 816e2c90 ffa4d418 00000000  Atmp.,n.........
```

この例では、複数のバッファーに完了している (の繰り返しのインスタンスで示される*DPC&lt;* ) が存在しない未処理のバッファー、キュー、プロセスのディスパッチが呼び出されないように (によって示される、休暇の*Prc&lt;* )。 実際には、すべてのキューに処理されたバッファーが完了したら、どうやら新しい未処理バッファーを追加する可能性があります。 アプリケーションが既に実行されているため (ように*開始*は呼び出されません) への呼び出しが行われないと*CallOnDPC* (があるため、処理済みのバッファーの準備がありませんが完了する)、新しいバッファーが何も処理を開始すると、処理待ちのリーディング エッジ事前累積ようです。

問題、KSPIN は\_フラグ\_は\_いない\_開始\_処理フラグが設定されています。 呼び出すことによってのみ処理が行われるときに、このフラグを設定すると、*開始*または*CallOnDPC*します。 このフラグが設定されていない場合は、新しいバッファーをキューに追加されるたびに処理が開始されます。

 

 





