---
title: バグチェック 0xC000021A WINLOGON_FATAL_ERROR
description: WINLOGON_FATAL_ERROR のバグチェックの値は0xC000021A です。 これは、Winlogon プロセスが予期せず終了したことを意味します。
ms.assetid: d46e2948-ff18-49e0-a738-7b90ab54d333
keywords:
- バグチェック 0xC000021A WINLOGON_FATAL_ERROR
- WINLOGON_FATAL_ERROR
ms.date: 09/12/2019
topic_type:
- apiref
api_name:
- WINLOGON_FATAL_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 13ae8b065d908615ffd66cd20cd130fbad73bd67
ms.sourcegitcommit: 6d7f25f280af5fd4f4d9337d131c2a22288847fc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72359577"
---
# <a name="bug-check-0xc000021a-winlogon_fatal_error"></a>バグチェック 0xC000021A: WINLOGON @ no__t-0FATAL @ no__t-1 エラー

WINLOGON @ no__t-0FATAL @ no__t エラーのバグチェックには、0xC000021A という値が指定されています。 これは、Winlogon プロセスが予期せず終了したことを意味します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。

## <a name="winlogon_fatal_error-parameters"></a>WINLOGON @ no__t-0FATAL @ no__t-1ERROR Parameters

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
<td align="left"><p>問題を識別する文字列</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>エラー コード</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="even">
<td align="left"><p>ホーム フォルダーが置かれているコンピューターにアクセスできない</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

<a name="cause"></a>原因
-----

このエラーは、WinLogon やクライアントサーバーの実行時サブシステム (CSRSS) などのユーザーモードサブシステムが致命的に侵害され、セキュリティを保証できなくなった場合に発生します。 応答として、オペレーティングシステムはカーネルモードに切り替わります。 Microsoft Windows は、WinLogon または CSRSS なしでは実行できません。 そのため、これは、ユーザーモードサービスのエラーによってシステムがシャットダウンされる可能性のあるいくつかのケースの1つです。

システムファイルが一致しないと、このエラーが発生することもあります。 この不一致は、バックアップからハードディスクを復元した場合に発生する可能性があります。 一部のバックアッププログラムでは、使用中のシステムファイルの復元をスキップする場合があります。

<a name="resolution"></a>解像度
----------

この状況では、ユーザーモードプロセスで実際のエラーが発生したため、カーネルデバッガーを実行しても役に立たない場合があります。

### <a name="resolving-an-error-in-a-user-mode-device-driver-system-service-or-third-party-application"></a>ユーザーモードデバイスドライバー、システムサービス、またはサードパーティ製のアプリケーションでのエラーの解決

バグチェック0xC000021A はユーザーモードプロセスで発生するため、最も一般的な発生はサードパーティ製のアプリケーションです。 新しいデバイスドライバー、システムサービス、またはサードパーティ製のアプリケーションをインストールした後にエラーが発生した場合は、新しいソフトウェアを削除するか無効にして、原因を特定する必要があります。 考えられる更新プログラムについて、ソフトウェアの製造元にお問い合わせください。

### <a name="resolving-a-mismatched-system-file-problem"></a>システムファイルが一致しない問題の解決

最近バックアップからハードディスクを復元した場合は、更新されたバージョンのバックアップ/復元プログラムが製造元から入手可能かどうかを確認してください。

- 最近インストールしたアプリケーションを確認します。 これを行うには、[コントロールパネル] の [プログラムのアンインストールと変更] に移動し、インストールされているアプリケーションをインストール日順に並べ替えます。

- エラーの原因となっているデバイスまたはドライバーの特定に役立つ可能性のある追加のエラーメッセージについては、イベントビューアーのシステムログを確認してください。 詳細については、「 [Open イベントビューアー](https://support.microsoft.com/hub/4338813/windows-help#1TC=windows-7)」を参照してください。 ブルースクリーンと同じ時間枠内に発生したシステムログの重大なエラーを探します。

-   エラーの原因となっているデバイスまたはドライバーの特定に役立つ可能性のある追加のエラーメッセージについては、イベントビューアーのシステムログを確認してください。 ブルースクリーンと同じ時間枠内に発生したシステムログの重大なエラーを探します。

<a name="remarks"></a>注釈
-------

- システムファイルチェッカーツールを使用して、システムファイルが見つからないか破損しているかを修復します。 システムファイルチェッカーは、windows のユーティリティであり、ユーザーが Windows システムファイルの破損をスキャンし、破損したファイルを復元できるようにします。 次のコマンドを使用して、システムファイルチェッカーツール (SFC.EXE) を実行します。

    ```console
    SFC /scannow
    ```

    詳細については、「[システムファイルチェッカーツールを使用したシステムファイルの不足または破損の修復」を](https://support.microsoft.com/help/929833/use-the-system-file-checker-tool-to-repair-missing-or-corrupted-system)参照してください。

-   ウイルス検出プログラムを実行します。 ウイルスは、Windows 用にフォーマットされたすべての種類のハードディスクに感染する可能性があり、その結果、ディスクの破損によってシステムのバグチェックコードが生成される可能性があります。 ウイルス検出プログラムがマスタブートレコードの感染を確認していることを確認します。

-   システムに最新の更新プログラムがインストールされていることを確認します。 システムにインストールされているバージョンを検出するには、 **[スタート]** ボタンをクリックし、 **[実行]** を選択して「 **winver**」と入力し、enter キーを押します。 [バージョン**情報**] ダイアログボックスには、windows のバージョン番号 (および Service Pack がインストールされている場合はバージョン番号) が表示されます。

### <a name="using-safe-mode"></a>セーフモードの使用

トラブルシューティングのために要素を分離し、必要に応じて Windows を使用するには、セーフモードを使用することを検討してください。 セーフモードを使用すると、Windows の起動時に最小限必要なドライバーとシステムサービスのみが読み込まれます。

セーフモードに移行するには、設定 で **更新とセキュリティ** を使用します。 メンテナンスモードで起動するには、[**回復**&nbsp; @ no__t **] を選択**します。 生成されたメニューで、 **[トラブルシューティング]** を選択し &nbsp; @ No__t の**詳細オプション**&nbsp; @ no__t**スタートアップ設定**&nbsp; @ no__t を**再起動**します。 Windows が再起動し、 **[スタートアップの設定]** 画面が表示されたら、オプション4、5、または6を選択してセーフモードで起動します。

セーフモードは、起動時にファンクションキーを押すことによって使用することもできます。たとえば、F8 キーを押します。 特定のスタートアップオプションについては、コンピューターの製造元の情報を参照してください。
