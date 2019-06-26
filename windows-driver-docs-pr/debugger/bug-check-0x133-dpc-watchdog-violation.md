---
title: バグ チェック 0x133 DPC_WATCHDOG_VIOLATION
description: DPC_WATCHDOG_VIOLATION のバグ チェックでは、0x00000133 の値を持ちます。
ms.assetid: CE9A4CBF-0016-42F7-A9EE-56DF6E61593A
keywords:
- バグ チェック 0x133 DPC_WATCHDOG_VIOLATION
- DPC_WATCHDOG_VIOLATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DPC_WATCHDOG_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b6573e5debe3eb5da8b994c1fe49f4aa713814dd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362250"
---
# <a name="bug-check-0x133-dpcwatchdogviolation"></a>バグ チェック 0x133 DPC\_ウォッチドッグ\_違反


DPC\_ウォッチドッグ\_違反のバグ チェックが 0x00000133 の値を持ちます。 このバグ チェックを示します、DPC ウォッチドッグが実行する、1 つの実行時間の長い遅延プロシージャ呼び出し (DPC) が検出されたか、またはシステムでは、長時間にわたる時間を費やして、割り込み要求レベル (IRQL) ためのディスパッチ\_レベルまたはそれ以降。 パラメーター 1 の値は、1 つの DPC が、タイムアウトを超えたかどうかを示す、システムが累積的 IRQL のディスパッチに長時間を費やしたかどうか、または\_レベルまたはそれ以降。 Dpc を 100 マイクロ秒より長く実行しないでくださいと Isr を 25 (マイクロ秒) よりも長く実行しないでください、ただし実際のタイムアウト値、システムは、非常に高いに設定されます。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)します。


## <a name="dpcwatchdogviolation-parameters"></a>DPC\_ウォッチドッグ\_違反パラメーター


*パラメーター 1*違反の種類を示します。 その他のパラメーターの意味は、の値によって異なります。*パラメーター 1*します。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター 1</th>
<th align="left">パラメータ 2</th>
<th align="left">3 番目のパラメーター</th>
<th align="left">パラメーター 4</th>
<th align="left">エラーの原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>(ティック) の DPC 時間のカウント</p></td>
<td align="left"><p>DPC 時間は、(ティック) に配分します。</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>1 つの DPC または ISR、その時間の配分を超えました。 問題が発生したコンポーネントは、スタック トレースでは、通常識別できます。</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>ウォッチドッグの期間</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>予約済み</p></td>
<td align="left"><p>システムには、長期間 IRQL DISPATCH_LEVEL 以上の時間の累積的に費やされました。 問題が発生したコンポーネントは、スタック トレースでは、通常識別できます。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

[ **! 分析**](-analyze.md)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるに役に立ちます。

**パラメーター 1 = 0**

この例では、501 のティック数は 500 の DPC 時間の単位を超えています。 イメージの名前は、バグ チェックが発生したときに、このコードが実行されていることを示します。

```dbgcmd
0: kd> !analyze -v
*******************************************************************************
*                                                                             *
*                        Bugcheck Analysis                                    *
*                                                                             *
*******************************************************************************

DPC_WATCHDOG_VIOLATION (133)
The DPC watchdog detected a prolonged run time at an IRQL of DISPATCH_LEVEL
or above.
Arguments:
Arg1: 0000000000000000, A single DPC or ISR exceeded its time allotment. The offending
    component can usually be identified with a stack trace.
Arg2: 0000000000000501, The DPC time count (in ticks).
Arg3: 0000000000000500, The DPC time allotment (in ticks).
Arg4: 0000000000000000

...

IMAGE_NAME:  BthA2DP.sys
...
```

0 のパラメーターを使用したエラーの詳細情報を収集するのにには、次のデバッガー コマンドを使用します。

[**k (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)停止コードが発生したときに実行されたどのようなコードを確認します。

詳細を掘り下げて u、ub の uu (Unassemble) コマンドを使用することも、コードを実行しています。

[ **! Pcr** ](-pcr.md)拡張機能は、特定のプロセッサのプロセッサ コントロール リージョン (PCR) の現在の状態を表示します。 出力は、Prcb のアドレスであります。

```dbgcmd
                     Prcb: fffff80309974180
```

使用することができます、 [ **dt (型の表示)** ](dt--display-type-.md) Dpc と DPC ウォッチドッグに関する追加情報を表示するコマンド。 アドレスの記載 Prcb を使用して、! pcr 出力。

```dbgcmd
dt nt!_KPRCB fffff80309974180 Dpc* 
```

**パラメーター 1 = 1**

1 のパラメーターに、コードはコードの問題のある領域に停止しません可能性があります。 ここで 1 つは、どのドライバーが通常の実行期間を超えているを追跡しようとするイベントのトレースを使用します。

詳細については、以下のトピックを参照してください。

[クラッシュ ダンプ分析の Windows デバッガー (WinDbg) の使用方法](crash-dump-files.md)

[WinDbg をカーネル モードのダンプ ファイルの分析](analyzing-a-kernel-mode-dump-file-with-windbg.md)

[使用して、! 拡張機能を分析](using-the--analyze-extension.md)と[! 分析](-analyze.md)

<a name="remarks"></a>注釈
-------

一般にこの停止コードは、障害のあるドライバー コードを特定の状況では、割り当てられた時間内には、その作業が完了しない原因です。

この問題を Windows デバッガーを使用する備えていない場合は、基本的なトラブルシューティングの手法を使用してください。

-   ドライバーにバグの確認メッセージで識別される場合は、この問題を分離するドライバー無効にします。 ドライバーの更新プログラムの製造元に確認してください。

-   デバイスまたは 0x133 のバグ チェックが原因となっているドライバーの特定に役立つ可能性がある追加のエラー メッセージをイベント ビューアーのシステム ログを確認します。

-   インストールされている新しいハードウェアが Windows のインストールされているバージョンと互換性があることを確認します。 たとえばに必要なハードウェアに関する情報を取得できます[Windows 10 の仕様](https://www.microsoft.com/windows/windows-10-specifications)します。

-   その他の一般的なトラブルシューティング情報を参照してください。 [**青い画面データ**](blue-screen-data.md)します。

 

 




