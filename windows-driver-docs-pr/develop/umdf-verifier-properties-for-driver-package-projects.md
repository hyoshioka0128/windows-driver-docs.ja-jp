---
ms.assetid: 5BF7AB90-FF2E-4679-8C84-2E8091917F5D
title: ドライバー パッケージ プロジェクトの UMDF 検証ツール プロパティ
description: テスト コンピューター上の UMDF 検証ツールのプロパティを設定します。 ドライバーをビルドしてテスト コンピューターに展開するときに、これらの設定を使うことができます。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9708097e195c7c8da785ae49e45008c20ed0d201
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518752"
---
# <a name="umdf-verifier-properties-for-driver-package-projects"></a>ドライバー パッケージ プロジェクトの UMDF 検証ツール プロパティ

テスト コンピューター上の UMDF 検証ツールのプロパティを設定します。 ドライバーをビルドしてテスト コンピューターに展開するときに、これらの設定を使うことができます。

展開について詳しくは、「[ドライバーの展開およびテストのためのコンピューターのプロビジョニング (WDK 8.1)](https://msdn.microsoft.com/Library/Windows/Hardware/Dn745909)」と「[テスト コンピューターへのドライバーの展開](deploying-a-driver-to-a-test-computer.md)」をご覧ください。

UMDF ドライバーのデバッグについて詳しくは、「[UMDF ドライバーのデバッグを有効にする方法](https://msdn.microsoft.com/Library/Windows/Hardware/Ff554716)」と「[WDF 検証ツールの制御アプリケーション](https://msdn.microsoft.com/Library/Windows/Hardware/Ff556129)」をご覧ください。

## <a name="span-idsettingumdfverifierpropertiesfordriverprojectsspanspan-idsettingumdfverifierpropertiesfordriverprojectsspanspan-idsettingumdfverifierpropertiesfordriverprojectsspansetting-umdf-verifier-properties-for-driver-projects"></a><span id="Setting_UMDF_Verifier_properties_for_driver_projects"></span><span id="setting_umdf_verifier_properties_for_driver_projects"></span><span id="SETTING_UMDF_VERIFIER_PROPERTIES_FOR_DRIVER_PROJECTS"></span>ドライバー プロジェクト用の UMDF 検証ツール プロパティの設定


1.  ドライバー パッケージのプロパティ ページを開きます。 ソリューション エクスプローラーでドライバー パッケージ プロジェクトを右クリックし、**[プロパティ]** をクリックします。
2.  ドライバー パッケージのプロパティ ページで、**[構成プロパティ]**、**[Driver Install]** (ドライバーのインストール)、**[UMDF Verifier]** (UMDF 検証ツール) の順にクリックします。
3.  **[Deploy UMDF Verifier] (UMDF 検証ツールを展開する)** オプションを選択します。 このオプションが有効 (**[はい]**) になっていると、UMDF 検証ツールのオプションを選択し、テスト コンピューターで使って、UMDF ドライバーを検証できます。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">構成方法</th>
<th align="left">説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="_Deploy_UMDF_Verifier"></span><span id="_deploy_umdf_verifier"></span><span id="_DEPLOY_UMDF_VERIFIER"></span><strong>Deploy UMDF Verifier (UMDF 検証ツールを展開する)</strong></p></td>
<td align="left"><p>テスト コンピューターで UMDF 検証ツールの設定を有効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="UMDF_Service_Names"></span><span id="umdf_service_names"></span><span id="UMDF_SERVICE_NAMES"></span><strong>UMDF Service Names (UMDF サービス名)</strong></p></td>
<td align="left"><p>監視対象の UMDF ドライバーのサービス名を指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Enable_Object_Tracking"></span><span id="enable_object_tracking"></span><span id="ENABLE_OBJECT_TRACKING"></span><strong>Enable Object Tracking (オブジェクトの追跡を有効にする)</strong></p></td>
<td align="left"><p>作成されたすべての UMDF オブジェクトを追跡します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Enable_Reference_Count_Tracking"></span><span id="enable_reference_count_tracking"></span><span id="ENABLE_REFERENCE_COUNT_TRACKING"></span><strong>Enable Reference Count Tracking (参照数の追跡を有効にする)</strong></p></td>
<td align="left"><p>すべての UMDF オブジェクト参照を追跡します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Maximum_Restart_Attempts"></span><span id="maximum_restart_attempts"></span><span id="MAXIMUM_RESTART_ATTEMPTS"></span><strong>Maximum Restart Attempts (再起動の最大試行回数)</strong></p></td>
<td align="left"><p>失敗したホスト プロセスを UMDF が再起動する最大回数です。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="UMDF_Logging_level"></span><span id="umdf_logging_level"></span><span id="UMDF_LOGGING_LEVEL"></span><strong>UMDF Logging level (UMDF ログ レベル)</strong></p></td>
<td align="left"><p>ホストしているドライバー用の UMDF 検証ツールでログに記録される情報の量を指定します。</p>
<p><strong>Only Critical and Fatal Errors (重大で致命的なエラーのみ)</strong> - 重大で致命的なエラーのみをログに記録します。</p>
<p><strong>All Errors (すべてのエラー)</strong> - すべてのエラーをログに記録します。</p>
<p><strong>Warnings and all Errors (警告とすべてのエラー)</strong> - 警告とすべてのエラーをログに記録します。</p>
<p><strong>Informational events, Warnings and all Errors (情報イベント、警告とすべてのエラー)</strong> - 情報イベント、警告、すべてのエラーをログに記録します。</p>
<p><strong>Verbose Output (All Events of any Sort) (詳細出力 (すべての種類のすべてのイベント))</strong> - すべてのイベントをログに記録します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Log_to_Kernel_Debugger"></span><span id="log_to_kernel_debugger"></span><span id="LOG_TO_KERNEL_DEBUGGER"></span><strong>Log to Kernel Debugger (カーネル デバッガーへのログの記録)</strong></p></td>
<td align="left"><p>検証ツールの出力をカーネル デバッガーのログに記録します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Break_into_Kernel_Debugger"></span><span id="break_into_kernel_debugger"></span><span id="BREAK_INTO_KERNEL_DEBUGGER"></span><strong>Break into Kernel Debugger (カーネル デバッガーへの割り込み)</strong></p></td>
<td align="left"><p>UMDF ホスト プロセスが失敗すると、カーネル デバッガーに割り込みます。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Attach_to_Kernel_Debugger"></span><span id="attach_to_kernel_debugger"></span><span id="ATTACH_TO_KERNEL_DEBUGGER"></span><strong>Attach to Kernel Debugger (カーネル デバッガーへのアタッチ)</strong></p></td>
<td align="left"><p>ユーザー モード デバッガーがアタッチされていない場合、カーネル デバッガーにアタッチします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Timeout_on_Driver_Load__sec_"></span><span id="timeout_on_driver_load__sec_"></span><span id="TIMEOUT_ON_DRIVER_LOAD__SEC_"></span><strong>Timeout on Driver Load (sec) (ドライバーの読み込みのタイムアウト (秒))</strong></p></td>
<td align="left"><p>ドライバーの読み込み後、デバッガーをアタッチするまでの待機時間 (単位: 秒) を指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Timeout_on_Driver_Start__sec_"></span><span id="timeout_on_driver_start__sec_"></span><span id="TIMEOUT_ON_DRIVER_START__SEC_"></span><strong>Timeout on Driver Start (sec) (ドライバーの開始のタイムアウト (秒))</strong></p></td>
<td align="left"><p>ドライバーの開始後、デバッガーをアタッチするまでの待機時間 (単位: 秒) を指定します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Verify_at_Current_Level"></span><span id="verify_at_current_level"></span><span id="VERIFY_AT_CURRENT_LEVEL"></span><strong>Verify at Current Level (現在のレベルでの確認)</strong></p></td>
<td align="left"><p>以前のバージョンのフレームワークを使ってビルドされたドライバーを、現在のフレームワーク バージョンのルールに対して確認します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


* [ユーザー モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)
* [ドライバーの検証ツール](https://msdn.microsoft.com/Library/Windows/Hardware/Ff545448)
* [テスト コンピューターへのドライバーの展開](deploying-a-driver-to-a-test-computer.md)
 

 






