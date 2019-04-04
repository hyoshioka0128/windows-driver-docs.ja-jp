---
title: バグ チェック 0x3B SYSTEM_SERVICE_EXCEPTION
description: SYSTEM_SERVICE_EXCEPTION のバグ チェックでは、0x0000003B の値を持ちます。 これは、特権のないコードから特権を持つコードに遷移するルーチンを実行中に例外が発生したことを示します。
ms.assetid: 0e2c230e-d942-4f32-ae8e-7a54aceb4c19
keywords:
- バグ チェック 0x3B SYSTEM_SERVICE_EXCEPTION
- SYSTEM_SERVICE_EXCEPTION
ms.date: 09/12/2018
topic_type:
- apiref
api_name:
- SYSTEM_SERVICE_EXCEPTION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 022950eb69951b70c4b514b961385d3c90a92e61
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572295"
---
# <a name="bug-check-0x3b-systemserviceexception"></a>バグ チェック 0x3B:システム\_サービス\_例外


システム\_サービス\_例外のバグ チェックが 0x0000003B の値を持ちます。 これは、特権のないコードから特権を持つコードに遷移するルーチンを実行中に例外が発生したことを示します。

**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

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

パラメーター 1 で返される例外情報が記載[NTSTATUS 値](https://msdn.microsoft.com/library/cc704588.aspx)は、Windows Driver Kit の inc ディレクトリにある ntstatus.h ファイルでも。 

可能性のある例外の 1 つの値は、0xC0000005 を示します。ステータス\_アクセス\_違反 

これは、メモリ アクセス違反が発生したことを意味します。 

[ **! 分析**](-analyze.md)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるには非常に役に立ちます。

詳細については、以下のトピックを参照してください。

[クラッシュ ダンプ分析の Windows デバッガー (WinDbg) の使用方法](crash-dump-files.md)

[WinDbg をカーネル モードのダンプ ファイルの分析](analyzing-a-kernel-mode-dump-file-with-windbg.md)

[使用して、! 拡張機能を分析](using-the--analyze-extension.md)と[! 分析](-analyze.md)


以前は、このエラーは、ページ プールの過剰な使用状況にリンクされているし、カーネル コード ユーザー モード グラフィックス ドライバー クロス オーバーを渡して不適切なデータことにより行われる可能性があります。 これは、大文字と小文字が疑われる場合は、追加情報を収集するドライバーの検証ツールのプール オプションを使用します。

<a name="resolution"></a>解決方法
----------

**この問題をデバッグします。** 使用して、 [ **.cxr (コンテキスト レコードの表示)** ](-cxr--display-context-record-.md)パラメーター 3 では、コマンドを使用して[ **kb (Display Stack Backtrace)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)します。 また、この停止コードに至るまで、コードにブレークポイントを設定、エラーが発生したコードをシングル ステップ転送しようし、することができますも。

Windows のバグの一般的なトラブルシューティングのコードを確認、これらの推奨事項に従ってください。

-   最近削除または置換することをお試し、システムにハードウェアを追加した場合 または、更新プログラムが利用可能な製造元に確認します。

-   新しいデバイス ドライバまたはシステム サービスを最近では、追加されている場合を削除するか、それらを更新してみてください。 表示する新しいチェック コードをバグの原因となったシステムで変更内容を調べてください。

-   検索対象**デバイス マネージャー**を任意のデバイスの感嘆符 (!) が付いてを参照してください。 任意のエラーが発生したドライバーのドライバーのプロパティに表示されるイベント ログを確認します。 関連するドライバーを更新してみてください。

-   デバイスまたはエラーの原因となっているドライバーの特定に役立つ可能性がある追加のエラー メッセージをイベント ビューアーのシステム ログを確認します。 詳細については、[イベント ビューアーを開く](https://windows.microsoft.com/windows/what-information-event-logs-event-viewer#1TC=windows-7)を参照してください。 ブルー スクリーンに同じ期間に発生したシステム ログの重大なエラーを探します。

-   その他の一般的なトラブルシューティング情報を参照してください。 [**青い画面データ**](blue-screen-data.md)します。

 

 




