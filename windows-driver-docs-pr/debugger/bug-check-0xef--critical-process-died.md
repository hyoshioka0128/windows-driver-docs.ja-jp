---
title: バグチェック 0xEF CRITICAL_PROCESS_DIED
description: CRITICAL_PROCESS_DIED のバグチェックの値は、0x000000EF です。 これは、重要なシステムプロセスが停止したことを示します。
ms.assetid: caa18221-6128-4d77-ab61-ef3c28cfba38
keywords:
- バグチェック 0xEF CRITICAL_PROCESS_DIED
- CRITICAL_PROCESS_DIED
ms.date: 02/25/2020
topic_type:
- apiref
api_name:
- CRITICAL_PROCESS_DIED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 657ff1747b3830370b2ba5a976425cdd5dd1386b
ms.sourcegitcommit: f1f641bd759b7bf6e45626ffcc090ffd28337c30
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/28/2020
ms.locfileid: "78166670"
---
# <a name="bug-check-0xef-critical_process_died"></a>バグチェック 0xEF: 重大な\_プロセス\_しています

CRITICAL_PROCESS_DIED のバグチェックの値は、0x000000EF です。 これは、重要なシステムプロセスが停止したことを示します。 重要なプロセスは、システムが終了するかどうかをバグチェックに強制するプロセスです。 これは、プロセスの状態が破損している場合、または破損している場合に発生する可能性があります。 このような状況が発生した場合、Windows の運用にはこれらのプロセスが不可欠であるため、システムのバグチェックはオペレーティングシステムの整合性に問題があると考えられます。 

Windows の重要なシステムサービスとしては、csrss、wininit.ini、logonui、smss、services.exe、services.exe、および winlogon が含まれています。

開発者は、サービスを作成し、その回復オプションを設定してコンピューターを再起動することもできます。詳細については、「[サービスが失敗したときに実行する回復アクションの設定](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753662(v=ws.11))」を参照してください。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。

## <a name="critical_process_died-parameters"></a>重大な\_プロセス\_のパラメーター

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
<td align="left"><p>Process オブジェクト</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>0の場合、プロセスは停止しています。 1の場合、スレッドは停止しています。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>予約済み</p></td>
</tr>
</tbody>
</table>

## <a name="resolution"></a>解決方法

この問題の原因を特定するには、通常、追加情報を収集するためにデバッガーを使用する必要があります。 複数のダンプファイルを調べて、stop コードが表示されたときに実行されているコードのように、この stop コードの特性が類似しているかどうかを確認する必要があります。

詳細については、「 [Windows デバッガー (WinDbg) を使用したクラッシュダンプ分析](crash-dump-files.md)」を参照してください。そのためには、 [! analyze 拡張機能](using-the--analyze-extension.md)と[! analyze](-analyze.md)を使用します。

多くの場合、システムのバグチェックの前にユーザーダンプも作成されます。  一般に、ユーザーダンプを利用できる場合は、まず問題の根本原因を調査する必要があります。 これは、ページアウト/欠損データを含む、カーネルダンプからのユーザーモードコードのデバッグに制限があるためです。 詳細については、「[ユーザーモードのダンプファイル](user-mode-dump-files.md)」を参照してください。 

イベントログを使用して、この stop コードに先行するエラーが発生していないかどうかを確認します。 存在する場合は、これらのエラーを使用して、調査する特定のサービスまたはその他のコードを調べることができます。

問題のコードに関する情報を入手できたら、このコードを実行する前に関連するコードにブレークポイントを設定し、コードフローの制御に使用される重要な変数の値を示すコードを1回順に進めます。  コードのこの領域を慎重に調べて、誤った想定やその他の誤りを見つけてください。 

バグチェックの2番目のパラメーターを使用して、起きプロセスまたはスレッドによってバグチェックが発生したかどうかを確認します。

プロセスの場合は、 [! process](-process.md)コマンドを使用して、異常な動作を検出するために失敗したポイントの前後にプロセスに関する情報を表示します。 [プロセスエクスプローラー](https://docs.microsoft.com/sysinternals/downloads/process-explorer)ユーティリティを使用すると、実行中のプロセスと親子関係に関する一般的な情報を収集できます。

スレッドの場合は、スレッドに関する情報を表示するために、 [! thread](-thread.md)コマンドを使用することを検討してください。 カーネルモードのスレッドの詳細については、「[コンテキストの変更](changing-contexts.md)」を参照してください。 

スレッドとプロセスに関する一般的な情報に加え、Windows で保護されている重要なコード (wininit.ini や csrss など) に関するその他の詳細については、「 *Windows 内部*での Pavel の使用」を参照してください。

## <a name="general-troubleshooting-tips"></a>一般的なトラブルシューティングのヒント

デバッガーを使用できない場合は、これらの一般的なトラブルシューティングのヒントが役に立つことがあります。

-   最近システムにハードウェアを追加した場合は、削除または交換してみてください。 または、製造元に確認して、修正プログラムが利用可能かどうかを確認してください。

-   新しいデバイスドライバーまたはシステムサービスが最近追加された場合は、それらを削除または更新してみてください。 新しいバグチェックコードが表示される原因となったシステムの変更内容を確認します。

-   エラーの原因となっているデバイスまたはドライバーの特定に役立つ可能性のある追加のエラーメッセージについては、イベントビューアーのシステムログを確認してください。 詳細については、「 [Open イベントビューアー](https://support.microsoft.com/hub/4338813/windows-help#1TC=windows-7)」を参照してください。 ブルースクリーンと同じ時間枠内に発生したシステムログの重大なエラーを探します。

-   製造元に確認して、更新されたシステム BIOS またはファームウェアが使用可能かどうかを確認してください。

-   システムの製造元から提供されているハードウェア診断を実行できます。

-   インストールされている新しいハードウェアに、インストールされている Windows のバージョンとの互換性があることを確認します。 たとえば、 [Windows 10 の仕様](https://www.microsoft.com/windows/windows-10-specifications)では、必要なハードウェアに関する情報を取得できます。

-   ウイルス検出プログラムを実行します。 ウイルスは、Windows 用にフォーマットされたすべての種類のハードディスクに感染し、ディスクの破損によってシステムのバグチェックコードが生成される可能性があります。 ウイルス検出プログラムがマスタブートレコードの感染を確認していることを確認します。

-   システムファイルチェッカーツールを使用して、システムファイルが見つからないか破損しているかを修復します。 システムファイルチェッカーは、windows のユーティリティであり、ユーザーが Windows システムファイルの破損をスキャンし、破損したファイルを復元できるようにします。 次のコマンドを使用して、システムファイルチェッカーツール (SFC.EXE) を実行します。

    ```console
    SFC /scannow
    ```

    詳細については、「[システムファイルチェッカーツールを使用したシステムファイルの不足または破損の修復」を](https://support.microsoft.com/help/929833/use-the-system-file-checker-tool-to-repair-missing-or-corrupted-system)参照してください。

-   **デバイスマネージャー**を検索して、感嘆符 (!) でマークされているデバイスがあるかどうかを確認します。 [ドライバーのプロパティ] に表示されている、エラーが発生しているドライバーのイベントログを確認します。 関連するドライバーを更新してみてください。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目

[Windows デバッガー (WinDbg) を使用したクラッシュダンプ分析](crash-dump-files.md)

[WinDbg を使用したカーネルモードのダンプファイルの分析](analyzing-a-kernel-mode-dump-file-with-windbg.md)
