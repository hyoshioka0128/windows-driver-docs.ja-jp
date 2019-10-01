---
title: バグチェック 0x3B SYSTEM_SERVICE_EXCEPTION
description: SYSTEM_SERVICE_EXCEPTION のバグチェックの値は0x0000003B です。 これは、特権のないコードから特権コードに遷移するルーチンの実行中に例外が発生したことを示します。
ms.assetid: 0e2c230e-d942-4f32-ae8e-7a54aceb4c19
keywords:
- バグチェック 0x3B SYSTEM_SERVICE_EXCEPTION
- SYSTEM_SERVICE_EXCEPTION
ms.date: 03/24/2019
topic_type:
- apiref
api_name:
- SYSTEM_SERVICE_EXCEPTION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5a3f803e82c3a2320c8ca2dd6829f863d260f29e
ms.sourcegitcommit: 645e42f3d8c59e249247d101d63681093f6522ee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "71705405"
---
# <a name="bug-check-0x3b-system_service_exception"></a>バグ チェック 0x3B:SYSTEM @ NO__T-0SERVICE @ NO__T-1 例外


システムの @ no__t-0SERVICE @ no__t 例外チェックの値は0x0000003B です。 これは、特権のないコードから特権コードに遷移するルーチンの実行中に例外が発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="system_service_exception-parameters"></a>SYSTEM @ no__t-0SERVICE @ no__t-1 例外パラメーター


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
<td align="left"><p>バグチェックの原因となった例外。 </p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>バグチェックの原因となった命令のアドレス。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>バグチェックの原因となった例外のコンテキストレコードのアドレス。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

Stop コードは、実行中のコードに例外があり、その下にあるスレッドがシステムスレッドであることを示しています。

パラメーター1で返された例外情報は、 [Ntstatus 値](https://docs.microsoft.com/openspecs/windows_protocols/ms-erref/596a1078-e883-4972-9bbc-49e60bebca55)に一覧表示されます。また、Windows Driver Kit の inc. ディレクトリにある ntstatus ファイルでも使用できます。 

一般的な例外コードは次のとおりです。

- 0x80000003:STATUS\_BREAKPOINT

カーネルデバッガーがシステムにアタッチされていないときに、ブレークポイントまたはアサートが発生しました。

- 0XC0000005STATUS\_ACCESS\_VIOLATION

メモリアクセス違反が発生しました。 (バグチェックのパラメーター4は、ドライバーがアクセスしようとしたアドレスです)。

<a name="resolution"></a>解決方法
----------

**この問題をデバッグするには:** 

パラメーター3を指定した[**cxr (コンテキストレコードの表示)** ](-cxr--display-context-record-.md)コマンドを使用し、 [**Kb (スタックバックトレースの表示)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)を使用します。 また、コード内でこの停止コードまでのブレークポイントを設定し、エラーが発生したコードへのシングルステップフォワードを試行することもできます。 [U, ub, uu (Unassemble)](u--unassemble-.md)コマンドを使用して、アセンブリプログラムコードを表示します。


! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。

```dbgcmd
SYSTEM_SERVICE_EXCEPTION (3b)
An exception happened while executing a system service routine.
Arguments:
Arg1: 00000000c0000005, Exception code that caused the bugcheck
Arg2: fffff802328375b0, Address of the instruction which caused the bugcheck
Arg3: ffff9c0a746c2330, Address of the context record for the exception that caused the bugcheck
Arg4: 0000000000000000, zero.
...
```

詳細については、以下のトピックを参照してください。

[! Analyze 拡張機能の使用](using-the--analyze-extension.md) 

[WinDbg を使用したカーネルモードのダンプファイルの分析](analyzing-a-kernel-mode-dump-file-with-windbg.md)

エラーを処理しているドライバーを識別できる場合は、その名前が青色の画面に出力され、メモリ内の場所 (PUNICODE @ no__t-0STRING) **KiBugCheckDriver**に格納されます。 デバッガーの[**dx (Display Debugger Object Model Expression)** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/dx--display-visualizer-variables-)コマンドを使用して、この-`dx KiBugCheckDriver` を表示できます。

パラメーター1の例外コードに関する情報を表示するには、 [! error](-error.md)拡張機能を使用します。

```dbgcmd
2: kd> !error 00000000c0000005
Error code: (NTSTATUS) 0xc0000005 (3221225477) - The instruction at 0x%p referenced memory at 0x%p. The memory could not be %s.
```

エラーが発生したときに実行されていたことに関する手掛かりについては、スタックテキストを参照してください。 複数のダンプファイルが使用可能な場合は、情報を比較して、スタック内の共通コードを探します。 [**Kb (スタックバックトレースの表示)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)などのデバッガーコマンドを使用して、エラーが発生しているコードを調査します。

メモリに読み込まれているモジュールの一覧を表示するには、`lm t n` を使用します。 

@No__t-0 およびを使用して、システムメモリの全般的な状態を確認します。 @No__t-0 および `!pool` コマンドを使用して、メモリの特定の領域を調べることもできます。 

以前は、このエラーは過剰なページングプールの使用に関連付けられており、ユーザーモードのグラフィックドライバーが過剰なデータをカーネルコードに渡すことによって発生する可能性があります。 この問題が発生していると思われる場合は、ドライバーの検証ツールのプールオプションを使用して、追加情報を収集します。

**ドライバーの検証ツール**

ドライバーの検証ツールは、ドライバーの動作を確認するためにリアルタイムで実行されるツールです。 たとえば、ドライバーの検証ツールは、メモリプールなどのメモリリソースの使用を確認します。 ドライバーコードの実行中にエラーが発生した場合は、ドライバーコードのその部分をさらに詳しく調査できるように、例外を事前に作成します。 Driver verifier マネージャーは Windows に組み込まれており、すべての Windows Pc で使用できます。 ドライバー検証マネージャーを起動するには、コマンドプロンプトで「 *Verifer* 」と入力します。 確認するドライバーを構成できます。 ドライバーを検証するコードは、実行中のオーバーヘッドを追加するので、可能な限り最小のドライバー数を試してみてください。 詳細については、「 [Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)」を参照してください。


<a name="remarks"></a>コメント
----------

Windows バグチェックコードの一般的なトラブルシューティングについては、次の推奨事項に従ってください。

-   新しいデバイスドライバーまたはシステムサービスが最近追加された場合は、それらを削除または更新してみてください。 新しいバグチェックコードが表示される原因となったシステムの変更内容を確認します。

-   **デバイスマネージャー**を検索して、感嘆符 (!) でマークされているデバイスがあるかどうかを確認します。 [ドライバーのプロパティ] に表示されている、エラーが発生しているドライバーのイベントログを確認します。 関連するドライバーを更新してみてください。

-   エラーの原因となっているデバイスまたはドライバーの特定に役立つ可能性のある追加のエラーメッセージについては、イベントビューアーのシステムログを確認してください。 詳細については、「 [Open イベントビューアー](https://support.microsoft.com/hub/4338813/windows-help#1TC=windows-7)」を参照してください。 ブルースクリーンと同じ時間枠内に発生したシステムログの重大なエラーを探します。

-   最近システムにハードウェアを追加した場合は、削除または交換してみてください。 または、製造元に確認して、修正プログラムが利用可能かどうかを確認してください。

-   一般的なトラブルシューティング情報については、「 [**Blue Screen Data**](blue-screen-data.md)」を参照してください。


 

 




