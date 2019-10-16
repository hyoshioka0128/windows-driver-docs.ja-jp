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
ms.openlocfilehash: 9f92b529d19650ff18e9faff211131bfbd86eee4
ms.sourcegitcommit: 6d7f25f280af5fd4f4d9337d131c2a22288847fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72359581"
---
# <a name="bug-check-0x3b-system_service_exception"></a>バグチェック 0x3B: SYSTEM @ no__t-0SERVICE @ no__t-1 例外

システムの @ no__t-0SERVICE @ no__t 例外チェックの値は0x0000003B です。 これは、特権のないコードから特権コードに遷移するルーチンの実行中に例外が発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="system_service_exception-parameters"></a>SYSTEM @ no__t-0SERVICE @ no__t-1 例外パラメーター

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
<td align="left"><p>ホーム フォルダーが置かれているコンピューターにアクセスできない</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>


<a name="cause"></a>原因
-----

この停止コードは、実行中のコードに例外があり、その下にあるスレッドがシステムスレッドであることを示しています。

パラメーター1で返される例外情報については、「 [NTSTATUS values](https://docs.microsoft.com/openspecs/windows_protocols/ms-erref/596a1078-e883-4972-9bbc-49e60bebca55)」を参照してください。 例外コードは、 [Windows Driver Kit](https://docs.microsoft.com/windows-hardware/drivers/)によって提供されるヘッダーファイルである、 *ntstatus*で定義されています。 (詳細については、「 [Windows Driver Kit のヘッダーファイル](../gettingstarted/header-files-in-the-windows-driver-kit.md)」を参照してください)。 

一般的な例外コードは次のとおりです。

- 0x80000003: STATUS @ no__t-0BREAKPOINT ポイント

    カーネルデバッガーがシステムにアタッチされていないときに、ブレークポイントまたはアサートが発生しました。

- 0xC0000005: STATUS @ no__t-0ACCESS @ no__t-1VIOLATION

    メモリアクセス違反が発生しました。 (バグチェックのパラメーター4は、ドライバーがアクセスしようとしたアドレスです)。

<a name="resolution"></a>解像度
----------

この問題をデバッグするには、パラメーター3を指定した[ **cxr** (コンテキストレコードの表示)](-cxr--display-context-record-.md)コマンドを使用し、 [ **kb** (スタックバックトレースの表示)](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)を使用します。 また、この stop コードの前にあるコードにブレークポイントを設定し、エラーが発生したコードへのシングルステップフォワードを試行することもできます。 アセンブリプログラムコードを表示するには、 [ **u**、 **ub**、 **uu** (unassemble)](u--unassemble-.md)の各コマンドを使用します。


[ **! Analyze**](-analyze.md)デバッガー拡張機能は、バグチェックに関する情報を表示し、根本原因を特定するのに役立ちます。 次の例は、 **! analyze**からの出力です。

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

WinDbg と **! analyze**の詳細については、次のトピックを参照してください。

 - [! Analyze 拡張機能の使用](using-the--analyze-extension.md) 

 - [WinDbg を使用したカーネルモードのダンプファイルの分析](analyzing-a-kernel-mode-dump-file-with-windbg.md)

### <a name="identify-the-driver"></a>ドライバーを識別する

エラーの原因となっているドライバーを識別できる場合は、その名前が青色の画面に出力され、メモリ内の場所 (PUNICODE @ no__t-0STRING) **KiBugCheckDriver**に格納されます。 [ **Dx** (display debugger object model expression)](https://docs.microsoft.com/windows-hardware/drivers/debugger/dx--display-visualizer-variables-)、デバッガーコマンドを使用して、次のように表示できます。 `dx KiBugCheckDriver`.

パラメーター1の例外コードに関する情報を表示するには、 [ **! error**](-error.md)拡張機能を使用します。 次に示すのは、 **! error**からの出力の例です。

```dbgcmd
2: kd> !error 00000000c0000005
Error code: (NTSTATUS) 0xc0000005 (3221225477) - The instruction at 0x%p referenced memory at 0x%p. The memory could not be %s.
```

エラー発生時の実行内容に関する手掛かりについては、「WinDbg」の**スタックテキスト**の出力を参照してください。 複数のダンプファイルが使用できる場合は、その情報を比較して、スタック内の共通コードを探します。 [ **Kb** (スタックバックトレースを表示)](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)などのデバッガーコマンドを使用して、エラーが発生しているコードを調査します。

次のコマンドを使用して、メモリに読み込まれているモジュールを一覧表示します。 **lm t n**

システムメモリの一般的な状態を調べるには、 **! memusage**を使用します。 また、コマンド **! pte**と **! pool**を使用して、メモリの特定の領域を調べることもできます。 

以前は、このエラーは、ページプールの過剰な使用に関連付けられています。これは、ユーザーモードのグラフィックスドライバーが過剰に処理され、カーネルコードに不適切なデータを渡すことが原因で発生する可能性があります。 この問題が発生していると思われる場合は、ドライバーの検証ツールのプールオプションを使用して、追加情報を収集します。

### <a name="driver-verifier"></a>ドライバーの検証ツール

ドライバーの検証ツールは、ドライバーの動作を確認するためにリアルタイムで実行されるツールです。 たとえば、ドライバーの検証ツールは、メモリプールなどのメモリリソースの使用を確認します。 ドライバーコードの実行中に発生したエラーを特定する場合は、ドライバーコードのその部分をさらに詳しく調査できるように、例外を事前に作成します。 Driver Verifier Manager は、Windows に組み込まれており、すべての Windows Pc で使用できます。 

ドライバー検証マネージャーを起動するには、コマンドプロンプトで「 **verifier** 」と入力します。 検証するドライバーを構成できます。 ドライバーを検証するコードは、実行中のオーバーヘッドを追加するので、可能な限り最小のドライバー数を確認してみてください。 詳細については、「 [Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)」を参照してください。


<a name="remarks"></a>注釈
-------

Windows バグチェックコードの一般的なトラブルシューティングについては、次の推奨事項に従ってください。

-   新しいデバイスドライバーまたはシステムサービスが最近追加された場合は、それらを削除または更新してみてください。 新しいバグチェックコードが表示される原因となったシステムの変更内容を確認します。

-   デバイスマネージャーを検索して、感嘆符 (!) でマークされているデバイスがあるかどうかを確認します。これは問題を示します。 エラーが発生したデバイスドライバーのプロパティに表示されているイベントログを確認します。 関連するドライバーを更新してみてください。

-   エラーの原因となっているデバイスまたはドライバーの特定に役立つ可能性のある追加のエラーメッセージについては、イベントビューアーのシステムログを確認してください。 ブルースクリーンと同じ時間枠内に発生したシステムログの重大なエラーを探します。

-   最近システムにハードウェアを追加した場合は、削除または交換してみてください。 または、製造元に確認して、修正プログラムが利用可能かどうかを確認してください。

一般的なトラブルシューティング情報については、「 [Blue screen data](blue-screen-data.md)」を参照してください。
