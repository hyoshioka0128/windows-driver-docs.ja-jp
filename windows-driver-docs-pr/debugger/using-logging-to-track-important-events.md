---
title: ログを使用した重要イベントの追跡
description: ログを使用した重要イベントの追跡
ms.assetid: 297336c2-85fb-4235-a7ab-0bbf571b8b98
keywords:
- カーネルストリーミングデバッグ、ビデオストリームの停止、ログ記録
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f269ba5baec6fe1b66d7377673e0c8a215672502
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534753"
---
# <a name="using-logging-to-track-important-events"></a>ログを使用した重要イベントの追跡


一般に、データは、イベント、ミニドライバーの処理、バッファー入力候補をトリガーすることによってのみ下流に移動されます。 ハングまたは失速の原因を特定するには、次のようにします。

- **Ksgate<em>Xxx</em> **の呼び出しが一致しないことを確認します。

- **Ks*Xxx*AttemptProcessing**の呼び出しが省略されていないかどうかを確認します。

- イベントのトリガーに関連するコードの問題を探します。これには、問題ストリームのピンフラグを参照するコードや、 **KsPinAttemptProcessing**を呼び出すコードなどが含まれます。

- 処理ディスパッチに関連するコードの問題を探します。特に、ハードウェアにキューに配置し、複製ポインターが作成される場所です。

- ドライバーの遅延プロシージャ呼び出し (DPC) に関連するコード内の問題を探します。特に、バッファーが完了した場所、または[Ksk Streamポインター delete](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerdelete)に対する呼び出しが行われます。

- ストリームのスタートアップコードに問題がないか調べます。

この情報を収集する最も効果的な方法は、処理、バッファーの取得 (ハードウェアの複製とプログラミングなど)、バッファーの解放 (複製の削除など)、すべてのゲート操作など、影響を受けるリージョンのすべてのログを記録することです。 この情報の大部分はタイミングに依存しており、メモリベースのログ記録または ETW が必要です。

メモリベースのローリングログを保持するには、次のコードを使用します。

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

次に、単純な "dc g ログ" を使用して、 \_ デバッガーの**g \_ ログ**配列の内容を表示します。

次の例では、上記のメモリベースのスキームを使用して、処理が停止した原因を特定します。 出力は、graphedt の AVStream ストリーミングシナリオからのものです。 次のミニドライバーイベントがログに記録されました。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">省略形</th>
<th align="left">Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>Strt</em></p></td>
<td align="left"><p>このイベントは、ミニドライバーが最初にミニドライバーの<em>開始</em>ディスパッチ内からデバイスのバッファーをキューに置いたときに発生します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>中国語&lt;</em></p></td>
<td align="left"><p>このイベントは、ミニドライバーの<em>プロセス</em>ディスパッチの開始時に発生します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>AddB</em></p></td>
<td align="left"><p>このイベントは、ミニドライバーが<em>プロセス</em>ディスパッチ内からデバイスにバッファーをキューに置いたときに発生します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>DPC&lt;</em></p></td>
<td align="left"><p>このイベントは、ミニドライバーの<em>Callondpc</em>の開始時に発生します。 これは、バッファーの完了を示します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>Atmp</em></p></td>
<td align="left"><p>このイベントは、ミニドライバーが DPC 内から<strong>KsPinAttemptProcessing</strong>に呼び出したときに発生します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>Dele</em></p></td>
<td align="left"><p>このイベントは、ミニドライバーが DPC 内からを呼び出して、複製ストリームポインターを削除したときに発生します。</p></td>
</tr>
</tbody>
</table>

 

ログの抜粋は次のとおりです。

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

この最初のログの抜粋は、通常のストリーミング状態を表します。 最初の行では、バッファー (*DPC &lt; *) を完了するためにミニドライバーの*callondpc*が呼び出されます。 バッファーは削除 (*Dele*) され、キューに未処理のバッファーがある場合 (*Atmp*)、 **KsPinAttemptProcessing**が呼び出されて先頭のエッジを移動します。 この場合、プロセスディスパッチ (*Prc &lt; *) の呼び出しによってわかるように、がありました。 さらに多くのバッファーがキュー (*Addb*) に追加され、シナリオ全体が繰り返されます。

次の抜粋では、ログの最後のエントリがストールの前に含まれています。

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

この例では、いくつかのバッファーが完了しています ( *DPC &lt; *の繰り返しインスタンスによって示されています) が、キューに未処理のバッファーがないため、プロセスディスパッチは呼び出されていません ( *Prc &lt; *がない場合に示されます)。 実際、キュー内の処理済みのバッファーはすべて完了しており、新しい未処理のバッファーを追加する前に行われていました。 アプリケーションが既に実行されており ( *Start*が呼び出されないため)、 *callondpc*に対する呼び出しが行われていないため (完了する準備ができている処理済みのバッファーがないため)、新しいバッファーは処理を待機しているため、処理を開始しても処理を開始しません。

問題は、KSPIN フラグによって \_ \_ \_ \_ \_ 処理フラグが設定されていないことです。 このフラグが設定されている場合、処理は*Start*または*callondpc*の呼び出しを通じてのみ行われます。 このフラグが設定されていない場合、新しいバッファーがキューに追加されるたびに処理が開始されます。

 

 





