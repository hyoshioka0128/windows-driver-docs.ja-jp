---
title: ログを使用した重要イベントの追跡
description: ログを使用した重要イベントの追跡
ms.assetid: 297336c2-85fb-4235-a7ab-0bbf571b8b98
keywords:
- カーネル デバッグ ストリーム、ビデオ ストリーム失速、ログ記録
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bb20d0d2880a08f635c67882b71761d52f65cc6
ms.sourcegitcommit: b25275c2662bfdbddd97718f47be9bd79e6f08df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/13/2019
ms.locfileid: "67866520"
---
# <a name="using-logging-to-track-important-events"></a>ログを使用した重要イベントの追跡


一般に、データは、イベント、ミニドライバーの処理、およびバッファーの入力候補をトリガーすることによってのみ下流移動されます。 ハングの原因を特定または停止します。

- 確認が一致しない**KsGate<em>Xxx</em>** 呼び出し。

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
```

単純なを使用して、"dc g\_ログ"の内容を表示、 **g\_ログ**デバッガーでの配列。

次の例では、上のメモリに基づくスキームを使用して、処理の停止の原因を特定します。 出力は graphedt で AVStream ストリーミングのシナリオです。 次のミニドライバー イベントがログに記録されました。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">省略形</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>エラー</em></p></td>
<td align="left"><p>このイベントは、まずキュー ミニドライバーの内からデバイスのバッファーに、ミニドライバーときに発生します。<em>開始</em>ディスパッチします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>中華人民共和国&lt;</em></p></td>
<td align="left"><p>このイベントは、のミニドライバーの開始時に発生します<em>プロセス</em>ディスパッチします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>AddB</em></p></td>
<td align="left"><p>このイベントは、内からデバイスにバッファー キューに入れ、ミニドライバーときに発生します。 その<em>プロセス</em>ディスパッチします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>DPC&lt;</em></p></td>
<td align="left"><p>このイベントは、のミニドライバーの開始時に発生します<em>CallOnDPC</em>します。 バッファーの完了を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>Atmp</em></p></td>
<td align="left"><p>このイベントに DPC 内から、ミニドライバーを呼び出すときに発生します。 <strong>KsPinAttemptProcessing</strong>します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>Dele</em></p></td>
<td align="left"><p>このイベントは、複製ストリーム ポインターを削除する DPC 内から、ミニドライバーの呼び出し時に発生します。</p></td>
</tr>
</tbody>
</table>

 

ログの抜粋は、次のとおりです。

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

 

 





