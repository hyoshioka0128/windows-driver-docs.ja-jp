---
title: バグ チェック 0xD1 します。
description: バグ チェックでは、0x000000D1 の値を持ちます。 これは、カーネル モード ドライバーは、プロセスが高すぎる IRQL でページング可能なメモリへのアクセスを試行したことを示します。
ms.assetid: 26cfd881-cc6e-4cc3-b464-e67d75700b96
keywords:
- バグ チェック 0xD1 します。
- DRIVER_IRQL_NOT_LESS_OR_EQUAL
ms.date: 03/28/2019
topic_type:
- apiref
api_name:
- DRIVER_IRQL_NOT_LESS_OR_EQUAL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c13dd820784cd03a995d42c235fd9074c7d065d9
ms.sourcegitcommit: b25275c2662bfdbddd97718f47be9bd79e6f08df
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/13/2019
ms.locfileid: "67866523"
---
# <a name="bug-check-0xd1-driverirqlnotlessorequal"></a>バグ チェック 0xD1:ドライバー\_IRQL\_いない\_少ない\_または\_と等しい


ドライバー\_IRQL\_いない\_少ない\_または\_等しいバグ チェックが 0x000000D1 の値を持ちます。 これは、カーネル モード ドライバーが高すぎる IRQL プロセス中にページング可能なメモリへのアクセスを試行したことを示します。 

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="driverirqlnotlessorequal-parameters"></a>ドライバー\_IRQL\_いない\_少ない\_または\_等しいパラメーター


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">パラメーター</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>参照されるメモリ。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>IRQL の参照時にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><strong>0:</strong>Read</p>
<p><strong>1:</strong>書き込み</p>
<p><strong>2:</strong>Execute</p>
<p><strong>8:</strong>Execute</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>メモリ アドレス。 このアドレスで 'ln' を使用して、関数の名前を参照してください。</p></td>
</tr>
</tbody>
</table>

<a name="cause"></a>原因
-----

ドライバーが、アドレスはページング可能な (または完全に有効でない) にアクセスしようとした通常の IRQL が高すぎます。

考えられる原因を以下に示します。

1. DISPATCH_LEVEL 以上で実行中に (NULL または解放されたポインターの場合) などの無効なポインターを逆参照します。
2. 同じか上位 DISPATCH_LEVEL ページング可能なデータにアクセスします。
3. 同じか上位 DISPATCH_LEVEL ページング可能なコードを実行しています。

その名前がブルー スクリーンに印刷し、場所のメモリに格納されている場合は、エラーのドライバーを識別できます (PUNICODE\_文字列) **KiBugCheckDriver**します。 Dx のデバッガー コマンドを使用するには、これを表示する`dx KiBugCheckDriver`します。

通常、このバグ チェックは不適切なメモリ アドレスを使用しているドライバーで発生します。

ページ フォールトの原因として、次のとおりです。

- この関数は、ページング可能としてマークされましたし、(ロックの取得が含まれています) を管理者特権での IRQL で実行されていた。

- 別のドライバーでの関数に対する関数呼び出しと、そのドライバーが読み込まれました。

- 無効なポインターを関数ポインターを使用して関数を呼び出しました。

<a name="resolution"></a>解決方法
----------

問題の原因が開発しているドライバーである場合は、そのバグ チェック時に実行された関数はページング可能としてマークされていないか、ページ アウトでした。 他のインライン関数を呼び出しませんを確認します。

[ **! 分析**](-analyze.md)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるに役に立ちます。

```dbgcmd
DRIVER_IRQL_NOT_LESS_OR_EQUAL (d1)
An attempt was made to access a pageable (or completely invalid) address at an
interrupt request level (IRQL) that is too high.  This is usually
caused by drivers using improper addresses.
If kernel debugger is available get stack backtrace.
Arguments:
Arg1: fffff808add27150, memory referenced
Arg2: 0000000000000002, IRQL
Arg3: 0000000000000000, value 0 = read operation, 1 = write operation
Arg4: fffff808adc386a6, address which referenced memory
```

トラップのフレームはダンプ ファイルの目的で使用可能なかどうか、`.trap`のコンテキストを指定したアドレスに設定するコマンド。

開始するには、スタック トレースを使用してを調べる、 [ **k、kb、kc、kd、kp、kP、kv (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンド。

使用して、`!IRQL`デバッガー中断する前に、ターゲット コンピューター上のプロセッサの割り込み要求レベル (IRQL) に関する情報を表示するコマンド。

```dbgcmd
0: kd> !irql
Debugger saved IRQL for processor 0x0 -- 2 (DISPATCH_LEVEL)
```

ほとんどの問題はなく、IRQL レベルでアクセスされているメモリではなくです。

このバグ チェックは、通常、不適切なメモリ アドレスを使用しているドライバーが原因であるためには、さらに 1, 3 および 4 invesitgate にパラメーターを使用します。

使用[ln (最も近いシンボルの一覧)](ln--list-nearest-symbols-.md)パラメーター 4 に、呼び出された関数の名前を参照してください。 確認も、! して、エラー コードが識別されるかどうかの出力を分析します。

使用[! プール](-pool.md)かどうか、それがページを参照してください。 へのパラメーター 1 アドレス プール。 使用[! アドレス](-address.md)と、高度な[! pte](-pte.md)詳細については、メモリのこの領域はコマンド。

使用して、[表示メモリ](-db---dc---dd---dp---dq---du---dw.md)パラメーター 1 でのコマンドで参照されているメモリを確認するためのコマンド。

使用して、 [Unassemble](u--unassemble-.md)コマンドをパラメーター 4 でのメモリをアドレスにコードを確認します。

使用して、`lm t n`メモリに読み込まれたモジュールを一覧表示します。 使用[! memusage](-memusage.md)と、システム メモリの [全般] の状態を確認します。 

**ドライバーの検証ツール**

Driver Verifier は、ドライバーの動作を確認するのにはリアルタイムで実行されているツールです。 たとえば、Driver Verifier は、メモリ プールなどのメモリ リソースの使用を確認します。 ドライバー コードの実行でエラーが表示される、さらに細かく検証するドライバー コードの部分を許可する例外が事前に作成されます。 ドライバー検証マネージャーは、Windows に組み込まれているしはすべての Windows Pc で使用できます。 ドライバー検証マネージャーを起動する入力*Verifer*コマンド プロンプトでします。 確認するにはどのドライバーを構成することができます。 ドライバーを検証するコードは実行時にオーバーヘッドを追加、のでお試しくださいし、可能なドライバーの最小数を確認します。 詳細については、次を参照してください。 [Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)します。

<a name="remarks"></a>コメント
-------

Windows デバッガーを使用してこの問題に取り組むを備えていない場合は、基本的なトラブルシューティングの手法を使用できます。

- デバイスまたはこのバグ チェックが原因となっているドライバーの特定に役立つ可能性がある追加のエラー メッセージをイベント ビューアーのシステム ログを確認します。

- バグ チェックのメッセージでドライバーが特定された場合は、そのドライバーを無効にするか、ドライバーの更新状況を製造元に確認します。

- インストールされている新しいハードウェアが Windows のインストールされているバージョンと互換性があることを確認します。 たとえばに必要なハードウェアに関する情報を取得できます[Windows 10 の仕様](https://www.microsoft.com/windows/windows-10-specifications)します。

- その他の一般的なトラブルシューティング情報を参照してください。 [**青い画面データ**](blue-screen-data.md)します。
