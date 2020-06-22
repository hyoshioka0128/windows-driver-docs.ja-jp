---
title: バグ チェック 0x3B SYSTEM_SERVICE_EXCEPTION
description: SYSTEM_SERVICE_EXCEPTION バグ チェックの値は 0x0000003B です。 これは、特権のないコードから特権コードに遷移するルーチンの実行中に例外が発生したことを示します。
ms.assetid: 0e2c230e-d942-4f32-ae8e-7a54aceb4c19
keywords:
- バグ チェック 0x3B SYSTEM_SERVICE_EXCEPTION
- SYSTEM_SERVICE_EXCEPTION
ms.date: 03/24/2019
topic_type:
- apiref
api_name:
- SYSTEM_SERVICE_EXCEPTION
api_type:
- NA
ms.localizationpriority: high
ms.openlocfilehash: 1ee9898b747fe08032107845c2167414eabca5e6
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534639"
---
# <a name="bug-check-0x3b-system_service_exception"></a>バグ チェック 0x3B:SYSTEM\_SERVICE\_EXCEPTION

SYSTEM\_SERVICE\_EXCEPTION バグ チェックの値は 0x0000003B です。 これは、特権のないコードから特権コードに遷移するルーチンの実行中に例外が発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 ユ―ザーとしてコンピューターを使用しているときにブルー スクリーン エラー コードが表示される場合は、[ブルー スクリーン エラーのトラブルシューティング](https://www.windows.com/stopcode)を参照してください。


## <a name="system_service_exception-parameters"></a>SYSTEM\_SERVICE\_EXCEPTION パラメーター

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
<td align="left"><p>バグ チェックの原因となった例外 </p></td>
</tr>
<tr class="even">
<td align="left"><p>2 で保護されたプロセスとして起動されました</p></td>
<td align="left"><p>バグ チェックの原因となった命令のアドレス</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>バグ チェックの原因となった例外のコンテキスト レコードのアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>


<a name="cause"></a>原因
-----

この停止コードは、実行中のコードに例外があり、その下にあるスレッドがシステムス レッドであることを示しています。

パラメーター 1 で返される例外情報については、「[NTSTATUS 値](https://docs.microsoft.com/openspecs/windows_protocols/ms-erref/596a1078-e883-4972-9bbc-49e60bebca55)」を参照してください。 例外コードは、[Windows Driver Kit](https://docs.microsoft.com/windows-hardware/drivers/) で提供されるヘッダー ファイル *ntstatus.h* に定義されています (詳細については、「[Windows Driver Kit のヘッダー ファイル](../gettingstarted/header-files-in-the-windows-driver-kit.md)」を参照してください)。 

一般的な例外コードは次のとおりです。

- 0x80000003:STATUS\_BREAKPOINT

    カーネル デバッガーがシステムにアタッチされていないときに、ブレークポイントまたはアサートが発生しました。

- 0xC0000005:STATUS\_ACCESS\_VIOLATION

    メモリ アクセス違反が発生しました (バグ チェックのパラメーター 4 は、ドライバーからアクセスが試行されたアドレスです)。

<a name="resolution"></a>解決方法
----------

この問題をデバッグするには、パラメーター 3 を指定して [ **.cxr** (コンテキスト レコードの表示)](-cxr--display-context-record-.md) コマンドを使用し、[**kb** (スタック バックトレースの表示)](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) を使用します。 また、この停止コードの前にあるコードにブレークポイントを設定し、エラーが発生したコードへのシングル ステップ フォワードを試行することもできます。 [**u**、**ub**、**uu** (unassemble)](u--unassemble-.md) コマンドを使用して、アセンブリ プログラム コードを表示します。


[ **!analyze**](-analyze.md) デバッガー拡張機能では、バグ チェックに関する情報が表示され、根本原因の特定に役立ちます。 次の例は **!analyze** からの出力です。

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

WinDbg および **!analyze** の詳細については、次のトピックを参照してください。

 - [!analyze 拡張機能の使用](using-the--analyze-extension.md) 

 - [WinDbg によるカーネルモード ダンプ ファイルの分析](analyzing-a-kernel-mode-dump-file-with-windbg.md)

### <a name="identify-the-driver"></a>ドライバーを特定する

エラーの原因となったドライバーを特定できる場合は、その名前がブルー スクリーンに出力され、メモリ内の場所 (PUNICODE\_STRING) **KiBugCheckDriver** に格納されます。 これを表示するには、[**dx** (デバッガー オブジェクト モデル式の表示)](dx--display-visualizer-variables-.md) デバッガーコマンドを使用します: `dx KiBugCheckDriver`。

[ **!error**](-error.md) 拡張機能を使用して、パラメーター 1 の例外コードに関する情報を表示します。 **!error** からの出力の例を次に示します。

```dbgcmd
2: kd> !error 00000000c0000005
Error code: (NTSTATUS) 0xc0000005 (3221225477) - The instruction at 0x%p referenced memory at 0x%p. The memory could not be %s.
```

エラーが発生したときに実行されていた内容の手掛かりについては、WinDbg からの **STACK TEXT** 出力を参照してください。 複数のダンプ ファイルが使用可能な場合は、それらの情報を比較して、スタック内の共通するコードを探します。 [**kb** (スタック バックトレースの表示)](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) などのデバッガー コマンドを使用して、エラーが発生したコードを確認します。

**lm t n** コマンドを使用して、メモリに読み込まれているモジュールを一覧表示します。

**!memusage** を使用して、システム メモリの全般的な状態を調べます。 また、コマンド **!pte** と **!pool** を使用して、特定のメモリ領域を調べることもできます。 

以前は、このエラーはページ プールの過剰な使用に関連付けられていました。これは、ユーザー モードのグラフィックス ドライバーが過剰に処理され、カーネル コードに不正なデータが渡されることが原因で発生する可能性があります。 このエラーが発生していると思われる場合は、ドライバーの検証ツールでプール オプションを使用して、追加情報を収集します。

### <a name="driver-verifier"></a>ドライバーの検証ツール

ドライバーの検証ツールは、リアルタイムで実行してドライバーの動作を調べるためのツールです。 たとえば、ドライバーの検証ツールでは、メモリ プールなどのメモリ リソースの使用がチェックされます。 ドライバー コードの実行でエラーが特定された場合は、ドライバー コードのその部分をさらに詳しく調査できるように、事前に例外が作成されます。 ドライバーの検証ツール マネージャーは、Windows に組み込まれており、すべての Windows PC で使用できます。 

ドライバーの検証マネージャーを起動するには、コマンドプロンプトで「**verifier**」と入力します。 どのドライバーを検証するかを構成できます。 ドライバーを検証するコードが実行されるとオーバーヘッドが増えるので、検証するドライバーの数を可能な限り少なくするようにしてください。 詳細については、「[ドライバーの検証ツール](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)」を参照してください。


<a name="remarks"></a>コメント
-------

Windows バグ チェック コードの一般的なトラブルシューティングについては、次の推奨事項に従ってください。

-   新しいデバイス ドライバーまたはシステム サービスが最近追加された場合は、それらを削除または更新してみてください。 新しいバグ チェック コードが表示される原因となったシステムの変更内容を確認します。

-   デバイス マネージャーを検索して、問題を示す感嘆符 (!) でマークされているデバイスがないか確認します。 エラーが発生したデバイス ドライバーのプロパティに表示されているイベント ログを確認します。 関連するドライバーを更新してみてください。

-   イベント ビューアーを使用してシステム ログで追加のエラー メッセージを確認すると、エラーの原因になっているデバイスやドライバーを特定できる可能性があります。 ブルー スクリーンと同じ時間帯に発生した重大なエラーをシステム ログで探します。

-   最近システムにハードウェアを追加した場合は、削除または交換してみてください。 または、利用可能なパッチがないか、製造元に確認します。

その他の一般的なトラブルシューティング情報については、「[ブルー スクリーンのデータ](blue-screen-data.md)」を参照してください。
