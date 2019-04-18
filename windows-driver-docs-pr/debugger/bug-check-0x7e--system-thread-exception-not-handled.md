---
title: バグ チェック 0x7E SYSTEM_THREAD_EXCEPTION_NOT_HANDLED
description: SYSTEM_THREAD_EXCEPTION_NOT_HANDLED のバグ チェックでは、0x0000007E の値を持ちます。 このバグ チェックでは、システム スレッドがエラー ハンドラーをキャッチされなかった例外を生成することを示します。
ms.assetid: 2ecea74f-21d6-4436-beed-d8cf8ef6b169
keywords:
- バグ チェック 0x7E SYSTEM_THREAD_EXCEPTION_NOT_HANDLED
- SYSTEM_THREAD_EXCEPTION_NOT_HANDLED
ms.date: 03/15/2019
topic_type:
- apiref
api_name:
- SYSTEM_THREAD_EXCEPTION_NOT_HANDLED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ae805605e03e4ac29c6784949351a9bb4de679f3
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/18/2019
ms.locfileid: "59239473"
---
# <a name="bug-check-0x7e-systemthreadexceptionnothandled"></a>バグ チェック 0x7E:システム\_スレッド\_例外\_いない\_処理済み


システム\_スレッド\_例外\_いない\_処理済みのバグ チェックが 0x0000007E の値を持ちます。 このバグ チェックでは、システム スレッドがエラー ハンドラーをキャッチされなかった例外を生成することを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。


## <a name="systemthreadexceptionnothandled-parameters"></a>システム\_スレッド\_例外\_いない\_処理済みのパラメーター


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
<td align="left"><p>処理されなかった例外コード</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>例外が発生したアドレス</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>例外レコードのアドレス</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>コンテキスト レコードのアドレス</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

システム\_スレッド\_例外\_いない\_処理済みのバグ チェックでは、システム スレッドがエラー ハンドラーをキャッチされなかった例外を生成することを示します。 その解釈は、どの例外が生成されたを指定する必要があります。

一般的な例外コードを以下に示します。

-   0x80000002:ステータス\_DATATYPE\_不整合は、アラインされていないデータの参照が検出されたことを示します。

-   0x80000003:ステータス\_ブレークポイントは、システムにカーネル デバッガーが関連付けられていない場合に、ブレークポイントまたはアサートが発生したことを示します。

-   0xC0000005:ステータス\_アクセス\_違反では、メモリ アクセス違反が発生したことを示します。

例外コードの完全な一覧は、Microsoft Windows Driver Kit (WDK) の inc ディレクトリにある Ntstatus.h ファイルを参照してください。

<a name="resolution"></a>解決方法
----------

この問題をデバッグする場合は、パラメーター 2 (例外のアドレス) は、ドライバーまたはこの問題の原因となった関数を識別する必要があります。

バグ チェック メッセージ内で名前によってドライバーがある場合は、無効にするか、またはそのドライバーを削除します。 問題は、1 つのドライバーに絞り込む、ブレークポイントを設定し、1 つがエラーを特定し、イベント、クラッシュにつながる洞察を得るに機能するコードのステップします。

[ **! 分析**](-analyze.md)バグ チェックに関する情報を表示拡張機能をデバッグおよび根本原因を突き止めるに役に立ちます。 

追加の分析を行うことができますを使用して、 [ **! スレッド**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-thread)拡張子だけでなく[ **dds、dp、dqs** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/dds--dps--dqs--display-words-and-symbols-)コマンド。 WinDbg のレポートするときに、適切な手法できます"おそらくにより: ntkrnlmp.exe" 

例外コード 0x80000003 が発生、アサーション、ハード コーディングされたブレークポイントにヒットした、システムで開始された場合、 **/NODEBUG**スイッチします。 この問題は頻繁に発生する必要があります。 これが繰り返し発生する場合は、カーネル デバッガーが接続されていることと、システムを使用してください。 こと、 **/debug**スイッチ。

例外コード 0x80000002 が発生した場合、トラップ フレームは、追加の情報を提供します。


詳細については、以下のトピックを参照してください。

[クラッシュ ダンプ分析の Windows デバッガー (WinDbg) の使用方法](crash-dump-files.md)

[WinDbg をカーネル モードのダンプ ファイルの分析](analyzing-a-kernel-mode-dump-file-with-windbg.md)

[使用して、! 拡張機能を分析](using-the--analyze-extension.md)と[! 分析](-analyze.md)


**旅行時間のトレース**

バグ チェックはオンデマンドで再現できる場合は、WinDbg のプレビューを使用してタイム トラベル トレースを取ることの可能性を調査します。 詳細については、次を参照してください。[タイム トラベルのデバッグ - 概要](time-travel-debugging-overview.md)します。


<a name="remarks"></a>注釈
----------

Windows デバッガーを使用してこの問題に取り組むを備えていない場合は、基本的なトラブルシューティング手法を使用する必要があります。

-   デバイスまたは 0x7E のバグ チェックが原因となっているドライバーの特定に役立つ可能性がある追加のエラー メッセージをイベント ビューアーのシステム ログを確認します。

-   バグ チェックのメッセージでドライバーが特定された場合は、そのドライバーを無効にするか、ドライバーの更新状況を製造元に確認します。

-   すべての ACPI またはその他のファームウェアの更新プログラムのハードウェア ベンダーに確認します。 システムの非互換性、メモリの競合および IRQ の競合などのハードウェアの問題には、このエラーを生成できます。

-   メモリ キャッシュ/シャドウ処理エラーを解決しようとする BIOS の無効にすることもできます。 システムの製造元が提供するハードウェア診断を実行することもあります。

-   インストールされている新しいハードウェアが Windows のインストールされているバージョンと互換性があることを確認します。 たとえばに必要なハードウェアに関する情報を取得できます[Windows 10 の仕様](https://www.microsoft.com/windows/windows-10-specifications)します。

-   その他の一般的なトラブルシューティング情報を参照してください。 [**青い画面データ**](blue-screen-data.md)します。


 




