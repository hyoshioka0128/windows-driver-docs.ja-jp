---
title: バグ チェック 0xD1 します。
description: バグ チェックでは、0x000000D1 の値を持ちます。 これは、カーネル モード ドライバーは、プロセスが高すぎる IRQL でページング可能なメモリへのアクセスを試行したことを示します。
ms.assetid: 26cfd881-cc6e-4cc3-b464-e67d75700b96
keywords:
- バグ チェック 0xD1 します。
- する
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_IRQL_NOT_LESS_OR_EQUAL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 394644d10612dec67a93c6da1452ae43cc55c8e5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531243"
---
# <a name="bug-check-0xd1-driverirqlnotlessorequal"></a>バグ チェック 0xD1 の。ドライバー\_IRQL\_いない\_少ない\_または\_と等しい


ドライバー\_IRQL\_いない\_少ない\_または\_等しいバグ チェックが 0x000000D1 の値を持ちます。 これは、カーネル モード ドライバーは、プロセスが高すぎる IRQL でページング可能なメモリへのアクセスを試行したことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

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
<td align="left"><p>参照されるメモリ</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>IRQL の参照時に</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><strong>0:</strong>Read</p>
<p><strong>1:</strong>書き込み</p>
<p><strong>8:</strong>実行する</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>メモリ アドレス</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

アドレスはページング可能な (または完全に有効ではない) にアクセスしようとしているドライバーの IRQL が高すぎます。

通常、このバグ チェックは不適切なアドレスを使用しているドライバーで発生します。

場合は、最初のパラメーターは、4 番目のパラメーターと同じ値を持つ、3 番目のパラメーターは、実行の操作、このバグ チェック コード自体がページ アウトされたときに、コードを実行しようとしていたドライバーが原因の場合です。ページ フォールトの原因として、次のとおりです。

-   この関数は、ページング可能としてマークされましたし、(ロックの取得が含まれています) を管理者特権での IRQL で実行されていた。

-   別のドライバーでの関数に対する関数呼び出しと、そのドライバーが読み込まれました。

-   無効なポインターを関数ポインターを使用して関数を呼び出しました。

<a name="resolution"></a>解決方法
----------

[ **! 分析**](-analyze.md)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるには非常に役に立ちます。

詳細については、次を参照してください[Windows デバッガー (WinDbg) を使用してクラッシュ ダンプ分析。](crash-dump-files.md)

開始するには、スタック トレースを使用してを調べる、 [ **k、kb、kc、kd、kp、kP、kv (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)コマンド。

問題の原因が開発しているドライバーである場合は、そのバグ チェック時に実行された関数はページング可能としてマークされていないか、ページ アウトでした。 他のインライン関数を呼び出しませんを確認します。

Windows デバッガーを使用してこの問題に取り組むを備えていない場合は、基本的なトラブルシューティングの手法を使用できます。

-   デバイスまたはこのバグ チェックが原因となっているドライバーの特定に役立つ可能性がある追加のエラー メッセージをイベント ビューアーのシステム ログを確認します。

-   バグ チェックのメッセージでドライバーが特定された場合は、そのドライバーを無効にするか、ドライバーの更新状況を製造元に確認します。

-   インストールされている新しいハードウェアが Windows のインストールされているバージョンと互換性があることを確認します。 たとえばに必要なハードウェアに関する情報を取得できます[Windows 10 の仕様](https://www.microsoft.com/windows/windows-10-specifications)します。

-   その他の一般的なトラブルシューティング情報を参照してください。 [**青い画面データ**](blue-screen-data.md)します。

 

 




