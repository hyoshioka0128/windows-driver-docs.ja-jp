---
title: バグ チェック 0xEF CRITICAL_PROCESS_DIED
description: CRITICAL_PROCESS_DIED のバグ チェックでは、0x000000EF の値を持ちます。 これは、重要なシステム プロセスが亡くなったを示します。
ms.assetid: caa18221-6128-4d77-ab61-ef3c28cfba38
keywords:
- (開発者向けコンテンツ)バグ チェック 0xEF CRITICAL_PROCESS_DIED
- CRITICAL_PROCESS_DIED
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- CRITICAL_PROCESS_DIED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 91fbf611e5250fc51f1c429f7a185858d0260253
ms.sourcegitcommit: 78bbc162dcf6eb5816afbfa8ac546722bb98c6c8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2019
ms.locfileid: "56582923"
---
# <a name="developer-content-bug-check-0xef-criticalprocessdied"></a>(開発者向けコンテンツ)バグ チェック 0xEF の。重要な\_プロセス\_DIED

CRITICAL_PROCESS_DIED のバグ チェックでは、0x000000EF の値を持ちます。 これは、重要なシステム プロセスが亡くなったを示します。 重要なプロセスとは、終了した場合に、バグ チェックを強制的にシステムです。 これは、プロセスの状態が壊れているか、それ以外の場合は、破損している場合に発生します。 このような場合、これらのプロセスが Windows の操作に不可欠なオペレーティング システムの整合性に問題がシステムのバグ チェックが発生します。 

構築された csrss.exe、wininit.exe、logonui.exe、smss.exe、services.exe、conhost.exe、および winlogon.exe Windows で重要なシステム サービスが含まれます。 

サービスとセットの詳細については、コンピューターを再起動するには、その回復オプションを参照してください、開発者は作成もできます。[回復操作を実行場所と、サービスが失敗したセットアップ](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc753662(v=ws.11))します。


**重要な**プログラマ向けのトピックです。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)します。

## <a name="criticalprocessdied-parameters"></a>重要な\_プロセス\_DIED パラメーター


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
<td align="left"><p>プロセス オブジェクト</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>0 の場合は、プロセスが失われました。 1 の場合は、スレッドが失われました。</p></td>
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

 

<a name="resolution"></a>解決方法
----------

この問題の原因は通常問題を判断するには、追加情報を収集するためにデバッガーを使用する必要があります。 複数のダンプ ファイルは、この停止コードが停止コードが表示されるときに実行されているコードなど、類似した特性を調べる必要があります。

詳細については、次を参照してください。 [Windows デバッガー (WinDbg) を使用してクラッシュ ダンプ分析](crash-dump-files.md)、[を使用して、! 拡張機能を分析](using-the--analyze-extension.md)と[! 分析](-analyze.md)します。

多くの場合、ユーザーのダンプもシステムでバグチェックする前に作成されます。  一般に、ユーザーのダンプが利用できる場合に調べる必要があります最初、問題の根本原因をします。 アウト/欠損データのページングを含む、カーネル ダンプからユーザー モード コードをデバッグする制限事項があるためにです。 詳細については、「[ユーザー モード ダンプ ファイル](user-mode-dump-files.md)します。 

発生したエラーがこの停止コードまで先頭に、イベント ログを使用してください。 ある場合、特定のサービスまたは調査するには、他のコードを確認するこれらのエラーを使用できます。

バグ チェックでは再現できる場合は、タイム トラベルのトレースを使用して、バグ チェックにつながるイベントを記録することを検討します。 詳細については、「[タイム トラベルのデバッグ - 概要](time-travel-debugging-overview.md)します。

コードの問題に関する情報が使用可能なこのコードが実行されると、1 つ一歩前進コード フローの制御に使用される重要な変数の値を調べるコードを使用する前に、関連のコードでブレークポイントを設定します。  慎重にコードを次の前提条件が false またはその他の間違いのこの領域を確認します。 

見つかったプロセスまたはスレッドにバグ チェックが原因となったかどうかを判断するのにには、バグのチェックの 2 番目のパラメーターを使用します。

プロセス場合を使用して、 [! プロセス](-process.md)異常な動作を検索する障害の発生時点の前後にプロセスの情報を表示するコマンド。 [Process explorer](https://docs.microsoft.com/sysinternals/downloads/process-explorer)のどのプロセスの詳細については、実行されている親子リレーションシップ [全般] の情報を収集するユーティリティを使用できます。

スレッドがある場合は、使用を検討して、 [! スレッド](-thread.md)スレッドに関する情報を表示するコマンド。 スレッドがカーネル モードについては、次を参照してください。[変更コンテキスト](changing-contexts.md)します。 

スレッドとプロセスについての一般的な情報として、保護されている Windows wininit csrss などの重要なコードの詳細についてを参照してください*Windows Internals* Pavel Yosifovich、E. のある Mark Russinovich、David A. Solomon、Alex して。Ionescu します。



**一般的なトラブルシューティングのヒント**

デバッガーを使用しない場合は、一般的なトラブルシューティングのヒントが役立つ場合があります。

-   最近削除または置換することをお試し、システムにハードウェアを追加した場合 または、更新プログラムが利用可能な製造元に確認します。

-   新しいデバイス ドライバまたはシステム サービスを最近では、追加されている場合を削除するか、それらを更新してみてください。 表示する新しいチェック コードをバグの原因となったシステムで変更内容を調べてください。

-   デバイスまたはエラーの原因となっているドライバーの特定に役立つ可能性がある追加のエラー メッセージをイベント ビューアーのシステム ログを確認します。 詳細については、次を参照してください。[イベント ビューアーを開く](https://windows.microsoft.com/windows/what-information-event-logs-event-viewer#1TC=windows-7)します。 ブルー スクリーンに同じ期間に発生したシステム ログの重大なエラーを探します。

-   製造元に問い合わせて、更新されたシステムの BIOS またはファームウェアが使用できるかどうかを確認します。

-   システム製造元から提供されたハードウェア診断を実行して確認することができます。

-   インストールされている新しいハードウェアが Windows のインストールされているバージョンと互換性があることを確認します。 たとえばに必要なハードウェアに関する情報を取得できます[Windows 10 の仕様](https://www.microsoft.com/windows/windows-10-specifications)します。

-   ウイルス検出プログラムを実行します。 ウイルスに感染する可能性、Windows 用にフォーマットされたハード_ディスクのすべての種類と、結果として得られるディスクの破損は、システムのバグ チェックのコードを生成できます。 ウイルス検出プログラムへの感染マスター ブート レコードのチェックを確認します。

-   システム ファイル チェッカー ツールを使用して、欠落または破損システム ファイルを修復します。 システム ファイル チェッカーは、ユーティリティは Windows ユーザーを Windows システム ファイルで破損をスキャンし、復元できるようにするには、ファイルが破損しています。 システム ファイル チェッカー (SFC.exe) ツールを実行するのにには、次のコマンドを使用します。

    ```console
    SFC /scannow
    ```

    詳細については、次を参照してください。[システム ファイル チェッカー ツールを使用してシステム ファイルの欠落または破損の修復](https://support.microsoft.com/kb/929833)します。

-   検索対象**デバイス マネージャー**を任意のデバイスの感嘆符 (!) が付いてを参照してください。 任意のエラーが発生したドライバーのドライバーのプロパティに表示されるイベント ログを確認します。 関連するドライバーを更新してみてください。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[クラッシュ ダンプ分析の Windows デバッガー (WinDbg) の使用方法](crash-dump-files.md)

[WinDbg をカーネル モードのダンプ ファイルの分析](analyzing-a-kernel-mode-dump-file-with-windbg.md)

 

 




