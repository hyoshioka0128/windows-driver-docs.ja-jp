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
ms.openlocfilehash: e30b3877219cbe8137fdc96ca3fb44232e452cc1
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534611"
---
# <a name="bug-check-0x7e-system_thread_exception_not_handled"></a>バグチェック 0x7E: システム \_ スレッド \_ 例外が \_ 処理されていません \_


システム \_ スレッド \_ 例外が \_ ハンドルされていません \_ バグチェックの値は0x0000007e です。 このバグチェックは、エラーハンドラーでキャッチされなかった例外がシステムスレッドによって生成されたことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。


## <a name="system_thread_exception_not_handled-parameters"></a>システム \_ スレッドの \_ 例外が \_ 処理されていない \_ パラメーター

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
<td align="left"><p>処理されなかった例外コード。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>例外が発生したアドレス。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>例外レコードのアドレス。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>コンテキストレコードのアドレス。</p></td>
</tr>
</tbody>
</table>

<a name="cause"></a>原因
-----

このバグチェックは、エラーハンドラーでキャッチされなかった例外がシステムスレッドによって生成されたことを示します。 これを解釈するには、生成された例外を特定する必要があります。

一般的な例外コードは次のとおりです。

- 0x80000002: ステータス \_ データ型の \_ 不整合は、整列されていないデータ参照が検出されたことを示します。

- 0x80000003: 状態 \_ ブレークポイントは、カーネルデバッガーがシステムにアタッチされていないときに、ブレークポイントが検出されたことを示します。

- 0xC0000005: 状態 \_ アクセス \_ 違反は、メモリアクセス違反が発生したことを示します。

例外コードの完全な一覧については、「 [NTSTATUS 値](https://docs.microsoft.com/openspecs/windows_protocols/ms-erref/596a1078-e883-4972-9bbc-49e60bebca55)」を参照してください。 例外コードは、 [Windows Driver Kit](https://docs.microsoft.com/windows-hardware/drivers/)によって提供されるヘッダーファイルである、 *ntstatus*で定義されています。 (詳細については、「 [Windows Driver Kit のヘッダーファイル](../gettingstarted/header-files-in-the-windows-driver-kit.md)」を参照してください)。 


<a name="resolution"></a>解像度
----------

この問題のデバッグを計画している場合は、例外アドレス (パラメーター 2) で、この問題の原因となったドライバーまたは機能を特定する必要があります。

バグチェックメッセージ内にドライバーが名前で表示されている場合は、そのドライバーを無効にするか削除します。 問題が1つのドライバーに絞り込まれている場合は、コードでブレークポイントとシングルステップフォワードを設定してエラーを特定し、クラッシュにつながるイベントについて洞察を得ます。

[**! Analyze**](-analyze.md)デバッガー拡張機能は、バグチェックに関する情報を表示し、根本原因を特定するのに役立ちます。 

追加の分析を行うには、 [**! スレッド**](-thread.md)拡張機能と、 [ **dds**、 **dps**、および**dqs** (表示語とシンボル)](dds--dps--dqs--display-words-and-symbols-.md)コマンドを使用します。 これは、WinDbg が "原因として考えられる可能性があります: ntkrnlmp" の場合に合理的な手法です。 

例外コード0x80000003 が発生した場合、ハードコーディングされたブレークポイントまたはアサーションがヒットしましたが、システムは **/NODEBUG**スイッチを使用して起動されました。 この問題は頻繁に発生することはありません。 繰り返し発生する場合は、カーネルデバッガーが接続されていて、システムが **/debug**スイッチで起動されていることを確認します。

例外コード0x80000002 が発生した場合、トラップフレームに追加情報が提供されます。

WinDbg と **! analyze**の詳細については、次のトピックを参照してください。

 - [WinDbg を使用してクラッシュダンプファイルを分析する](crash-dump-files.md)

 - [WinDbg を使用したカーネルモードのダンプファイルの分析](analyzing-a-kernel-mode-dump-file-with-windbg.md)

 - [! Analyze 拡張機能](using-the--analyze-extension.md)と[! Analyze](-analyze.md)を使用する


<a name="remarks"></a>注釈
-------

Windows デバッガーを使用してこの問題に対処することができない場合は、いくつかの基本的なトラブルシューティング手法を使用する必要があります。

-   バグチェック0x7E の原因となっているデバイスまたはドライバーを特定するのに役立つ追加のエラーメッセージについては、イベントビューアーのシステムログを確認してください。

-   バグ チェックのメッセージでドライバーが特定された場合は、そのドライバーを無効にするか、ドライバーの更新状況を製造元に確認します。

-   ACPI またはその他のファームウェアの更新については、ハードウェアベンダーに確認してください。 システムの非互換性、メモリの競合、および IRQ の競合などのハードウェアの問題によって、このエラーが発生することもあります。

-   また、BIOS のメモリのキャッシュとシャドウを無効にして、エラーを解決することもできます。 また、システムの製造元が提供するハードウェア診断も実行します。

-   インストールされている新しいハードウェアに、インストールされている Windows のバージョンとの互換性があることを確認します。 たとえば、 [Windows 10 の仕様](https://www.microsoft.com/windows/windows-10-specifications)では、必要なハードウェアに関する情報を取得できます。

一般的なトラブルシューティング情報については、「 [Blue screen data](blue-screen-data.md)」を参照してください。
