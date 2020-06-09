---
title: バグチェック 0xD1 DRIVER_IRQL_NOT_LESS_OR_EQUAL
description: DRIVER_IRQL_NOT_LESS_OR_EQUAL バグチェックの値は0x000000D1 です。 これは、カーネルモードドライバーが、高すぎるプロセス IRQL でページング可能なメモリにアクセスしようとしたことを示します。
ms.assetid: 26cfd881-cc6e-4cc3-b464-e67d75700b96
keywords:
- バグチェック 0xD1 DRIVER_IRQL_NOT_LESS_OR_EQUAL
- DRIVER_IRQL_NOT_LESS_OR_EQUAL
ms.date: 03/28/2019
topic_type:
- apiref
api_name:
- DRIVER_IRQL_NOT_LESS_OR_EQUAL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9d18dd3f24300037011dc615ae61814ddae10d73
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534577"
---
# <a name="bug-check-0xd1-driver_irql_not_less_or_equal"></a>バグチェック 0xD1: ドライバー \_ の IRQL が \_ \_ 少ない \_ か \_ 等しい


ドライバーの \_ IRQL \_ が \_ 低い \_ か \_ 等しいバグチェックには、0x000000D1 の値が含まれています。 これは、カーネルモードドライバーが、プロセス IRQL が高すぎるときに、ページング可能なメモリにアクセスしようとしたことを示します。 

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="driver_irql_not_less_or_equal-parameters"></a>ドライバー \_ \_ の IRQL \_ が \_ パラメーターの値以下 \_

<table>
<colgroup>
<col width="20%" />
<col width="80%" />
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
<td align="left"><p>メモリが参照されています。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>参照時の IRQL。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><ul>
<li>0-読み取り</li>
<li>1-書き込み</li>
<li>2-実行</li>
<li>8-実行</li>
</td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>参照されたメモリをアドレスします。 関数の名前を表示するには、このアドレスに<a href="./ln--list-nearest-symbols-.md"> <strong>ln</strong> (一番近くにあるシンボルの一覧)</a>を使用します。</p></td>
</tr>
</tbody>
</table>


<a name="cause"></a>原因
-----

通常、このエラーが発生した場合、ドライバーは、割り込み要求レベル (IRQL) が高すぎたときに、ページング可能な (または完全に無効な) アドレスにアクセスしようとしました。 考えられる原因を以下に示します。

 - DISPATCH_LEVEL 以上の実行中に無効なポインター (NULL または解放されたポインターなど) を逆参照しています。

 - DISPATCH_LEVEL 以上のページング可能なデータへのアクセス。

 - DISPATCH_LEVEL 以上のページング可能なコードを実行しています。

エラーの原因となっているドライバーを識別できる場合は、その名前がブルースクリーンに出力され、メモリ内の場所 (PUNICODE \_ 文字列) **KiBugCheckDriver**に格納されます。 Dx KiBugCheckDriver を使用すると、デバッガーコマンドである[ **dx** (display debugger object model expression)](dx--display-visualizer-variables-.md)を使用して、 **dx**を表示できます。

このバグチェックは通常、不適切なメモリアドレスを使用したドライバーによって発生します。

ページフォールトには、次のような原因が考えられます。

- 関数は、ページング可能としてマークされ、管理者特権で実行されていました (ロックの取得を含む)。

- 関数呼び出しが別のドライバーの関数に対して行われましたが、そのドライバーはアンロードされました。

- 無効なポインターであった関数ポインターを使用して関数が呼び出されました。


<a name="resolution"></a>解像度
----------

開発中のドライバーが問題の原因である場合は、バグチェックの時点で実行されていた関数が (1) ページング可能としてマークされていないことを確認します。または、(2) は、ページングされている他のインライン関数を呼び出しません。

[**! Analyze**](-analyze.md)デバッガー拡張機能は、バグチェックに関する情報を表示し、根本原因を特定するのに役立ちます。 次の例は、 **! analyze**からの出力です。

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

ダンプファイルでトラップフレームが使用可能な場合は、 [**. trap**](-trap--display-trap-frame-.md)コマンドを使用して、指定されたアドレスにコンテキストを設定します。

この種類のバグチェックのデバッグを開始するには、 [ **k**、 **kb**、 **kc**、 **kd**、 **kp**、 **kp**、 **kv** (表示スタックバックトレース)](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)の各コマンドを使用して、スタックトレースを確認します。

デバッガーで[**! irql**](-irql.md)コマンドを実行して、デバッガーが中断する前にターゲットコンピューター上のプロセッサの irql に関する情報を表示します。 次に例を示します。

```dbgcmd
0: kd> !irql
Debugger saved IRQL for processor 0x0 -- 2 (DISPATCH_LEVEL)
```

この種のバグチェックの大部分では、問題は IRQL レベルではなく、アクセスされているメモリであることを示しています。

このバグチェックは通常、不適切なメモリアドレスを使用しているドライバーによって発生するため、パラメーター1、3、および4を使用してさらに調査を行います。

関数の名前を表示するには、パラメーター4を指定して[ **ln** (一番近くにあるシンボルの一覧)](ln--list-nearest-symbols-.md)を使用します。 また、 **! analyze**出力を調べて、エラーコードが特定されているかどうかを確認します。

パラメーター1のアドレスに対して[**! pool**](-pool.md)を使用して、ページプールであるかどうかを確認します。 このメモリ領域の詳細については、 [**! address**](-address.md)と advanced [**! pte**](-pte.md)コマンドを使用してください。

[[メモリの表示](-db---dc---dd---dp---dq---du---dw.md)] コマンドを使用して、パラメーター1のコマンドで参照されているメモリを確認します。

[ **U**、 **ub**、 **uu** (unassemble)](u--unassemble-.md)の各コマンドを使用して、パラメーター4のメモリを参照しているアドレス内のコードを確認します。

コマンドを使用して `lm t n` 、メモリに読み込まれているモジュールの一覧を表示します。 [**! Memusage**](-memusage.md)およびを使用して、システムメモリの一般的な状態を確認します。 


### <a name="driver-verifier"></a>ドライバーの検証ツール

ドライバーの検証ツールは、ドライバーの動作を確認するためにリアルタイムで実行されるツールです。 たとえば、ドライバーの検証ツールは、メモリプールなどのメモリリソースの使用を確認します。 ドライバーコードの実行中に発生したエラーを特定する場合は、ドライバーコードのその部分をさらに詳しく調査できるように、例外を事前に作成します。 Driver Verifier Manager は、Windows に組み込まれており、すべての Windows Pc で使用できます。

ドライバー検証マネージャーを起動するには、コマンドプロンプトで「 **verifier** 」と入力します。 検証するドライバーを構成できます。 ドライバーを検証するコードは、実行中のオーバーヘッドを追加するので、可能な限り最小のドライバー数を確認してみてください。 詳細については、「 [Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)」を参照してください。


<a name="remarks"></a>解説
-------

Windows デバッガーを使用してこの問題に対処することができない場合は、いくつかの基本的なトラブルシューティング手法を使用できます。

- このバグチェックの原因となっているデバイスまたはドライバーの特定に役立つ可能性のある追加のエラーメッセージについては、イベントビューアーのシステムログを確認してください。

- バグ チェックのメッセージでドライバーが特定された場合は、そのドライバーを無効にするか、ドライバーの更新状況を製造元に確認します。

- インストールされている新しいハードウェアに、インストールされている Windows のバージョンとの互換性があることを確認します。 たとえば、 [Windows 10 の仕様](https://www.microsoft.com/windows/windows-10-specifications)では、必要なハードウェアに関する情報を取得できます。

一般的なトラブルシューティング情報については、「 [Blue screen data](blue-screen-data.md)」を参照してください。
