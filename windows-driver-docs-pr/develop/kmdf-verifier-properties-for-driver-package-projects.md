---
ms.assetid: 40D39F8E-3CD3-434B-A161-45D5BD4FBA09
title: ドライバー パッケージ プロジェクトの KMDF 検証ツール プロパティ
description: リモート コンピューター上の KMDF 検証ツールのプロパティを設定します。  これらの設定を使って、KMDF ドライバーをビルドし、テスト コンピューターに展開します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ae1c204b9819dc9039de47a8af54396894b3159
ms.sourcegitcommit: dabd74b55ce26f2e1c99c440cea2da9ea7d8b62c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/13/2019
ms.locfileid: "63344134"
---
# <a name="kmdf-verifier-properties-for-driver-package-projects"></a>ドライバー パッケージ プロジェクトの KMDF 検証ツール プロパティ

リモート コンピューター上の KMDF 検証ツール (またはフレームワーク検証ツール) のプロパティを設定します。 KMDF ドライバーをビルドしてテスト コンピューターに展開するときに、これらの設定を使うことができます。 KMDF ドライバーについて詳しくは、「[カーネル モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)」をご覧ください。

フレームワーク検証ツールについて詳しくは、「[フレームワーク検証ツールの使用](https://msdn.microsoft.com/Library/Windows/Hardware/Ff545540)」と「[WDF 検証ツールの制御アプリケーション](https://msdn.microsoft.com/Library/Windows/Hardware/Ff556129)」をご覧ください。

## <a name="span-idsettingkmdfverifierpropertiesfordriverpackageprojectsspanspan-idsettingkmdfverifierpropertiesfordriverpackageprojectsspanspan-idsettingkmdfverifierpropertiesfordriverpackageprojectsspansetting-kmdf-verifier-properties-for-driver-package-projects"></a><span id="Setting_KMDF_Verifier_properties_for_driver_package_projects"></span><span id="setting_kmdf_verifier_properties_for_driver_package_projects"></span><span id="SETTING_KMDF_VERIFIER_PROPERTIES_FOR_DRIVER_PACKAGE_PROJECTS"></span>ドライバー パッケージ プロジェクトの KMDF 検証ツール プロパティの設定


1.  ドライバー パッケージのプロパティ ページを開きます。 ソリューション エクスプローラーでドライバー パッケージ プロジェクトを右クリックし、 **[プロパティ]** をクリックします。
2.  ドライバー パッケージのプロパティ ページで、 **[構成プロパティ]** 、 **[Driver Install]** (ドライバーのインストール)、 **[KMDF Verifier]** (KMDF 検証ツール) の順にクリックします。
3.  **[Enable KMDF Verifier]** (KMDF 検証ツールを有効にする) オプションをクリックし、 **[KMDF verifier is always on]** (KMDF 検証ツールは常にオン) を選びます。 このオプションがオンになっている場合は、KMDF ドライバーのフレームワーク検証オプションを構成できます。

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
<td align="left"><p><span id="Enable_KMDF_Verifier"></span><span id="enable_kmdf_verifier"></span><span id="ENABLE_KMDF_VERIFIER"></span><strong>Enable KMDF Verifier (KMDF 検証ツールを有効にする)</strong></p></td>
<td align="left"><p>テスト コンピューターで KMDF 検証ツールを有効にします。 選択できるオプションは、<strong>[KMDF verifier is always on] (KMDF 検証ツールは常にオン)</strong> または <strong>[KMDF verifer is off] (KMDF 検証ツールはオフ)</strong> です。 KMDF 検証ツールが有効になっていなくて KMDF のバージョンが 1.9 以上である場合、基本的なフレームワークの検証は、<a href="https://msdn.microsoft.com/Library/Windows/Hardware/Ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/Library/Windows/Hardware/Ff545448)">ドライバーの検証ツール</a>の一部として有効になります。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="KMDF_Service_Names"></span><span id="kmdf_service_names"></span><span id="KMDF_SERVICE_NAMES"></span><strong>KMDF Service Names (KMDF サービス名)</strong></p></td>
<td align="left"><p>監視対象の KDMF ドライバーのサービス名を指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="IRQL_checks"></span><span id="irql_checks"></span><span id="IRQL_CHECKS"></span><strong>IRQL checks (IRQL チェック)</strong></p></td>
<td align="left"><p>IRQL チェックと重大なメモリ リークのチェックを有効にします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Forward_Compatible_Checks"></span><span id="forward_compatible_checks"></span><span id="FORWARD_COMPATIBLE_CHECKS"></span><strong>Forward Compatible Checks (上位互換性チェック)</strong></p></td>
<td align="left"><p>現在のドライバーのバージョンより後に作られたチェックを有効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Forward_Progress_Handler_Testing"></span><span id="forward_progress_handler_testing"></span><span id="FORWARD_PROGRESS_HANDLER_TESTING"></span><strong>Forward Progress Handler Testing (進捗ハンドラー テスト)</strong></p></td>
<td align="left"><p>ドライバーの進捗処理テストのオプションを指定します。</p>
<p><strong>No Allocation Failures (割り当てエラーなし)</strong> エラーをシミュレートせずに、ドライバーの進捗処理をテストします。</p>
<p><strong>Fail All Allocations (すべての割り当てが失敗)</strong> ドライバーの進捗処理に依存して、進捗キューへのすべての I/O 要求が失敗したように表示されます。</p>
<p><strong>Randomly Fail Allocations (ランダムに割り当てが失敗)</strong> 進捗キューへの I/O 要求がランダムに失敗します。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Track_KMDF_Object_Handles"></span><span id="track_kmdf_object_handles"></span><span id="TRACK_KMDF_OBJECT_HANDLES"></span><strong>Track KMDF Object Handles (KMDF オブジェクト ハンドルを追跡する)</strong></p></td>
<td align="left"><p>追跡するオブジェクト ハンドルの種類の一覧を指定します。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Enable_KMDF_Loader_Messages"></span><span id="enable_kmdf_loader_messages"></span><span id="ENABLE_KMDF_LOADER_MESSAGES"></span><strong>Enable KMDF Loader Messages (KMDF ローダー メッセージを有効にする)</strong></p></td>
<td align="left"><p>デバッガーを使って KMDF ローダー メッセージを有効にします。 このオプションを有効にするには、ターゲット コンピューターの再起動が必要です。</p>
<p>Windows Vista 以降のオペレーション システムでは、既定で DbgPrint 出力が抑制されています。これにより、この抑制が無効になるまで、WDF ローダーの診断メッセージは使用できません。 KDMF 検証ツールはこれを管理して、KMDF ローダーの診断がこれらのシステムのカーネル デバッガーで使用できるようにします。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Verbose_logging"></span><span id="verbose_logging"></span><span id="VERBOSE_LOGGING"></span><strong>Verbose logging (詳細ログ)</strong></p></td>
<td align="left"><p>詳細なログを有効にします。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><span id="Memory_Pages_for_Logs"></span><span id="memory_pages_for_logs"></span><span id="MEMORY_PAGES_FOR_LOGS"></span><strong>Memory Pages for Logs (ログのメモリ ページ)</strong></p></td>
<td align="left"><p>カーネルのイベント トレース ログ用に、非ページ プール ページの数 (1 ～ 10) を指定して割り当てます。 オプションは、<strong>[Runtime Choice (ランタイムが選択)]</strong> または [<strong>1</strong>-<strong> 10</strong>] です。 <strong>[Runtime Choice (ランタイムが選択)]</strong> の場合、ページ数は KMDF ランタイムによって決まります。 KMDF 1.9 以降、検証が詳細ログと共に有効になっていると、ランタイムはより多くのページを使います。</p></td>
</tr>
<tr class="even">
<td align="left"><p><span id="Fail_Memory_Allocations"></span><span id="fail_memory_allocations"></span><span id="FAIL_MEMORY_ALLOCATIONS"></span><strong>Fail Memory Allocations (メモリ割り当ての失敗)</strong></p></td>
<td align="left"><p>KMDF 検証ツールが開始されてすべてのメモリ割り当てが失敗する前に、正常に割り当てできるメモリの数を指定します。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


* [カーネル モード ドライバー フレームワーク](https://docs.microsoft.com/windows-hardware/drivers/wdf/)
* [ドライバー検証ツール](https://msdn.microsoft.com/Library/Windows/Hardware/Ff545448)
* [テスト コンピューターへのドライバーの展開](deploying-a-driver-to-a-test-computer.md)
 

 






