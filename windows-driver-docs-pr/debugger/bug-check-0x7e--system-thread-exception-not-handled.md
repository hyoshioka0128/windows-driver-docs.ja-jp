---
title: バグチェック 0x7E SYSTEM_THREAD_EXCEPTION_NOT_HANDLED
description: SYSTEM_THREAD_EXCEPTION_NOT_HANDLED のバグチェックの値は0x0000007E です。 このバグチェックは、エラーハンドラーでキャッチされなかった例外がシステムスレッドによって生成されたことを示します。
ms.assetid: 2ecea74f-21d6-4436-beed-d8cf8ef6b169
keywords:
- バグチェック 0x7E SYSTEM_THREAD_EXCEPTION_NOT_HANDLED
- SYSTEM_THREAD_EXCEPTION_NOT_HANDLED
ms.date: 03/15/2019
topic_type:
- apiref
api_name:
- SYSTEM_THREAD_EXCEPTION_NOT_HANDLED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a503ecbbc796f182b1915283f41368d9d7ef755e
ms.sourcegitcommit: e7e5d959f4f6a23b3be46b6f7bdfc9da9bb08746
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/30/2019
ms.locfileid: "70025316"
---
# <a name="bug-check-0x7e-system_thread_exception_not_handled"></a>バグ チェック 0x7E:システム @ NO__T-0THREAD @ NO__T 例外 @ NO__T-2NOT @ NO__T-3HANDLED


システムの @ no__t-0THREAD @ no__t-1EXCEPTION @ no__t-2NOT @ no__t-3HANDLED @ のバグチェックの値は0x0000007E です。 このバグチェックは、エラーハンドラーでキャッチされなかった例外がシステムスレッドによって生成されたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。

## <a name="system_thread_exception_not_handled-parameters"></a>システム @ no__t-0THREAD @ no__t 例外 @ no__t-2NOT @ no__t-3HANDLED されたパラメーター

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
<td align="left"><p>コンテキストレコードのアドレス</p></td>
</tr>
</tbody>
</table>

<a name="cause"></a>原因
-----

システムの @ no__t-0THREAD @ no__t-1EXCEPTION @ no__t-2NOT @ no__t-3HANDLED bug check は、システムスレッドがエラーハンドラーでキャッチされなかった例外を生成したことを示します。 これを解釈するには、生成された例外を特定する必要があります。

一般的な例外コードは次のとおりです。

- 0x80000002状態 @ no__t-0DATATYPE @ no__t-1MISALIGNMENT は、整列されていないデータ参照が検出されたことを示します。

- 0x80000003:STATUS @ no__t-0BREAKPOINT ポイントは、カーネルデバッガーがシステムにアタッチされていないときに、ブレークポイントが検出されたことを示します。

- 0XC0000005STATUS @ no__t-0ACCESS @ no__t-1VIOLATION は、メモリアクセス違反が発生したことを示します。

例外コードの完全な一覧については、Microsoft Windows Driver Kit (WDK) の inc. のディレクトリにある Ntstatus ファイルを参照してください。

<a name="resolution"></a>解決方法
----------

この問題のデバッグを計画している場合は、パラメーター 2 (例外アドレス) で、この問題の原因となったドライバーまたは機能を特定する必要があります。

バグチェックメッセージ内にドライバーが名前で表示されている場合は、そのドライバーを無効にするか削除します。 問題が1つのドライバーに絞り込まれている場合は、コードにブレークポイントと単一ステップを設定して、障害を特定し、クラッシュにつながるイベントに関する洞察を得ます。

! [デバッグ拡張機能の[**分析**](-analyze.md)] には、バグチェックに関する情報が表示され、根本原因を特定するのに役立ちます。 

さらに、 [ **! スレッド**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-thread)拡張機能と、 [**dds、dps、dqs**](https://docs.microsoft.com/windows-hardware/drivers/debugger/dds--dps--dqs--display-words-and-symbols-)コマンドを使用して、追加の分析を行うことができます。 これは、WinDbg が "考えられる原因: ntkrnlmp" である可能性があるため、合理的な手法です。 

例外コード0x80000003 が発生した場合、ハードコーディングされたブレークポイントまたはアサーションがヒットしましたが、システムは **/NODEBUG**スイッチを使用して起動されました。 この問題は頻繁に発生することはありません。 繰り返し発生する場合は、カーネルデバッガーが接続されていて、システムが **/debug**スイッチで起動されていることを確認します。

例外コード0x80000002 が発生した場合、トラップフレームに追加情報が提供されます。

詳細については、以下のトピックを参照してください。

[Windows デバッガー (WinDbg) を使用したクラッシュダンプ分析](crash-dump-files.md)

[WinDbg を使用したカーネルモードのダンプファイルの分析](analyzing-a-kernel-mode-dump-file-with-windbg.md)

[! Analyze 拡張機能](using-the--analyze-extension.md)と[! Analyze](-analyze.md)を使用する

<a name="remarks"></a>コメント
----------

Windows デバッガーを使用してこの問題に対処することができない場合は、いくつかの基本的なトラブルシューティング手法を使用する必要があります。

- バグチェック0x7E の原因となっているデバイスまたはドライバーを特定するのに役立つ追加のエラーメッセージについては、イベントビューアーのシステムログを確認してください。

- バグ チェックのメッセージでドライバーが特定された場合は、そのドライバーを無効にするか、ドライバーの更新状況を製造元に確認します。

- ACPI またはその他のファームウェアの更新については、ハードウェアベンダーに確認してください。 システムの非互換性、メモリの競合、および IRQ の競合などのハードウェアの問題によって、このエラーが発生することもあります。

- また、BIOS のメモリのキャッシュとシャドウを無効にして、エラーを解決することもできます。 また、システムの製造元から提供されているハードウェア診断も実行する必要があります。

- インストールされている新しいハードウェアに、インストールされている Windows のバージョンとの互換性があることを確認します。 たとえば、 [Windows 10 の仕様](https://www.microsoft.com/windows/windows-10-specifications)では、必要なハードウェアに関する情報を取得できます。

- 一般的なトラブルシューティング情報については、「 [**Blue Screen Data**](blue-screen-data.md)」を参照してください。
