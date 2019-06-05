---
title: バグ チェック 0x3B SYSTEM_SERVICE_EXCEPTION
description: SYSTEM_SERVICE_EXCEPTION のバグ チェックでは、0x0000003B の値を持ちます。 これは、特権のないコードから特権を持つコードに遷移するルーチンを実行中に例外が発生したことを示します。
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
ms.localizationpriority: medium
ms.openlocfilehash: ca0c17cfccd665eb7f2d9af5ebcf0c6749303361
ms.sourcegitcommit: 5523bbb8b8bbeaabee8243ff8efc206aeebae5ea
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2019
ms.locfileid: "66515933"
---
# <a name="bug-check-0x3b-systemserviceexception"></a>バグ チェック 0x3B:システム\_サービス\_例外


システム\_サービス\_例外のバグ チェックが 0x0000003B の値を持ちます。 これは、特権のないコードから特権を持つコードに遷移するルーチンを実行中に例外が発生したことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="systemserviceexception-parameters"></a>システム\_サービス\_例外パラメーター


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
<td align="left"><p>バグ チェックを原因となった例外。 </p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
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

停止コードでは、例外が発生し、その下にあったスレッドがあったコードを実行することを示すシステム スレッドです。

パラメーター 1 で返される例外情報が記載[NTSTATUS 値](https://docs.microsoft.com/openspecs/windows_protocols/ms-erref/596a1078-e883-4972-9bbc-49e60bebca55)は、Windows Driver Kit の inc ディレクトリにある ntstatus.h ファイルでも。 

一般的な例外コードは次のとおりです。

-   0x80000003:ステータス\_ブレークポイント

    システムにカーネル デバッガーが関連付けられていない場合、ブレークポイントまたはアサートが発生しました。

-   0xC0000005:ステータス\_アクセス\_違反

    メモリ アクセス違反が発生しました。 (パラメーター 4 のバグ チェックは、ドライバーにアクセスしようとするアドレスです)。

<a name="resolution"></a>解決方法
----------

**この問題をデバッグします。** 

使用して、 [ **.cxr (コンテキスト レコードの表示)** ](-cxr--display-context-record-.md)パラメーター 3 では、コマンドを使用して[ **kb (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)します。 また、この停止コードに至るまで、コードにブレークポイントを設定、エラーが発生したコードをシングル ステップ転送しようし、することができますも。 使用して、 [u、ub、uu (Unassemble)]()コマンドをアセンブリのプログラム コードを参照してください。


[ **! 分析**](-analyze.md)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるに役に立ちます。

```
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

[使用して、! 拡張機能の分析](using-the--analyze-extension.md) 

[WinDbg をカーネル モードのダンプ ファイルの分析](analyzing-a-kernel-mode-dump-file-with-windbg.md)

その名前がブルー スクリーンに印刷し、場所のメモリに格納されている場合は、エラーのドライバーを識別できます (PUNICODE\_文字列) **KiBugCheckDriver**します。 デバッガーを使用する[ **dx (表示デバッガー オブジェクト モデル表現)** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/dx--display-visualizer-variables-) - これを表示するコマンドを`dx KiBugCheckDriver`します。

使用して、 [! エラー](-error.md)パラメーター 1 で、例外コードに関する情報を表示する拡張機能。

```
2: kd> !error 00000000c0000005
Error code: (NTSTATUS) 0xc0000005 (3221225477) - The instruction at 0x%p referenced memory at 0x%p. The memory could not be %s.
```

障害が発生したときに実行されていたものでスタック テキスト手がかりを確認します。 複数のダンプ ファイルが使用可能な場合は、情報を探す、スタックに共通のコードを比較します。 使用率などのデバッガー コマンドを使用して[ **kb (Display Stack Backtrace)** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)エラーが発生したコードを調査します。

使用して、`lm t n`メモリに読み込まれたモジュールを一覧表示します。 

使用`!memusage`と、システム メモリの [全般] の状態を確認します。 `!pte`と`!pool`コマンドがメモリの特定の領域を確認することも可能性があります。 

以前は、このエラーは、ページ プールの過剰な使用状況にリンクされているし、カーネル コード ユーザー モード グラフィックス ドライバー クロス オーバーを渡して不適切なデータことにより行われる可能性があります。 これは、大文字と小文字が疑われる場合は、追加情報を収集するドライバーの検証ツールのプール オプションを使用します。

**ドライバーの検証ツール**

Driver Verifier は、ドライバーの動作を確認するのにはリアルタイムで実行されているツールです。 たとえば、Driver Verifier は、メモリ プールなどのメモリ リソースの使用を確認します。 ドライバー コードの実行でエラーが表示される、さらに細かく検証するドライバー コードの部分を許可する例外が事前に作成されます。 ドライバー検証マネージャーは、Windows に組み込まれているしはすべての Windows Pc で使用できます。 ドライバー検証マネージャーを起動する入力*Verifer*コマンド プロンプトでします。 確認するにはどのドライバーを構成することができます。 ドライバーを検証するコードは実行時にオーバーヘッドを追加、のでお試しくださいし、可能なドライバーの最小数を確認します。 詳細については、次を参照してください。 [Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)します。


**旅行時間のトレース**

バグ チェックはオンデマンドで再現できる場合は、WinDbg のプレビューを使用してタイム トラベル トレースを取ることの可能性を調査します。 詳細については、次を参照してください。[タイム トラベルのデバッグ - 概要](time-travel-debugging-overview.md)します。


<a name="remarks"></a>注釈
----------

Windows のバグの一般的なトラブルシューティングのコードを確認、これらの推奨事項に従ってください。

-   新しいデバイス ドライバまたはシステム サービスを最近では、追加されている場合を削除するか、それらを更新してみてください。 表示する新しいチェック コードをバグの原因となったシステムで変更内容を調べてください。

-   検索対象**デバイス マネージャー**を任意のデバイスの感嘆符 (!) が付いてを参照してください。 任意のエラーが発生したドライバーのドライバーのプロパティに表示されるイベント ログを確認します。 関連するドライバーを更新してみてください。

-   デバイスまたはエラーの原因となっているドライバーの特定に役立つ可能性がある追加のエラー メッセージをイベント ビューアーのシステム ログを確認します。 詳細については、次を参照してください。[イベント ビューアーを開く](https://windows.microsoft.com/windows/what-information-event-logs-event-viewer#1TC=windows-7)します。 ブルー スクリーンに同じ期間に発生したシステム ログの重大なエラーを探します。

-   最近削除または置換することをお試し、システムにハードウェアを追加した場合 または、更新プログラムが利用可能な製造元に確認します。

-   その他の一般的なトラブルシューティング情報を参照してください。 [**青い画面データ**](blue-screen-data.md)します。


 

 




