---
title: ドライバーの検証ツールのオプションの選択
description: ドライバーの検証ツールのオプションの選択
ms.assetid: 02ef5dd6-7532-4979-b45c-a9ee81582788
keywords:
- Driver Verifier の WDK、オプションの選択
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2b0fd151576001898b1d1dce5f8658f855dce27
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351214"
---
# <a name="selecting-driver-verifier-options"></a>ドライバーの検証ツールのオプションの選択


## <span id="ddk_selecting_driver_verifier_options_tools"></span><span id="DDK_SELECTING_DRIVER_VERIFIER_OPTIONS_TOOLS"></span>


使用してドライバー検証ツールのオプションを選択することができます、 [ **Verifier のコマンド ライン**](verifier-command-line.md)、またはドライバー検証マネージャーを使用しています。 2 つのバージョンのドライバー検証マネージャー--に 1 つずつ[Windows 2000](driver-verifier-manager--windows-2000-.md)とに 1 つずつ[Windows XP 以降](driver-verifier-manager--windows-xp-and-later-.md)。

### <a name="span-idverifiercommandlinespanspan-idverifiercommandlinespanverifier-command-line"></a><span id="verifier_command_line"></span><span id="VERIFIER_COMMAND_LINE"></span>検証ツールのコマンドライン

アクティブ化または個別のオプションを非アクティブ化、後に必要なオプションを指定します、 **/flags**パラメーター。

(Windows 2000 のみ)I/O の検証のレベルを制御するには、使用、 **/iolevel**パラメーター。

(Windows XP 以降)標準のオプションをアクティブ化する[特別なプール](special-pool.md)、[強制 IRQL 検査](force-irql-checking.md)、[プール追跡](pool-tracking.md)、 [I/O の検証](i-o-verification.md)、 [DMA の検証](dma-verification.md)、および[デッドロック検出](deadlock-detection.md)--を使用して、 **標準/** パラメーター。 Windows Vista 以降、標準のオプションも含まれます[セキュリティ チェック](security-checks.md)と[(その他) を確認します](miscellaneous-checks.md)します。 Windows 8 以降、標準のオプションはそのも含める[DDI 準拠の検査](ddi-compliance-checking.md)します。

(Windows Server 2003 以降)アクティブ化する[ディスクの整合性チェック](disk-integrity-checking.md)を使用して、 **/ディスク**パラメーター。

すべてのオプションを非アクティブ化して、検証済みのドライバーの一覧を消去を使用して、 **/リセット**パラメーター。

参照してください[ **Verifier のコマンド ライン**](verifier-command-line.md)詳細についてはします。

### <a name="span-iddriververifiermanagerwindows2000spanspan-iddriververifiermanagerwindows2000spandriver-verifier-manager-windows-2000"></a><span id="driver_verifier_manager__windows_2000_"></span><span id="DRIVER_VERIFIER_MANAGER__WINDOWS_2000_"></span>ドライバー検証マネージャー (Windows 2000)

アクティブ化または個別のオプションを非アクティブ化は、選択、**設定**タブ。Driver Verifier のオプションが記載されて、**検証型**セクション ([特別なプール](special-pool.md)、[強制 IRQL 検査](force-irql-checking.md)、[低リソース シミュレーション](low-resources-simulation.md)、[プールの追跡](pool-tracking.md)、および[I/O の検証](i-o-verification.md))。 非アクティブ化するどのオプションを使用しをアクティブ化することを確認します。 I/O の検証が選択されている場合は、レベル 1 および Level 2 の (レベル 2 では、レベル 1 およびレベル 2 のテストの両方を選択する) の間で選択できます。 検証する必要のあるドライバーを選択するを参照してください。[検証するドライバーを選択すると](selecting-drivers-to-be-verified.md)します。

標準のオプションを有効にする[特別なプール](special-pool.md)、[強制 IRQL 検査](force-irql-checking.md)、[プール追跡](pool-tracking.md)、および[I/O の検証](i-o-verification.md)レベル 2 - の選択**設定**タブ。キーを押して、**優先設定**ボタンをクリックします。 このボタンを押すとも、**すべてのドライバーを確認します**オプション ボタンをクリックします。 検証済みのドライバーの一覧を変更するを参照してください場合、[検証するドライバーを選択すると](selecting-drivers-to-be-verified.md)、それ以外のキーを押して**適用**します。

すべてのオプションを非アクティブ化し、検証済みのドライバーの一覧をクリア、選択、**設定**タブ。キーを押して、**すべて元に戻す**ボタンをクリックします。 キーを押します**適用**します。

### <a name="span-iddriververifiermanagerwindowsxpandlaterspanspan-iddriververifiermanagerwindowsxpandlaterspandriver-verifier-manager-windows-xp-and-later"></a><span id="driver_verifier_manager__windows_xp_and_later_"></span><span id="DRIVER_VERIFIER_MANAGER__WINDOWS_XP_AND_LATER_"></span>ドライバー検証マネージャー (Windows XP 以降)

Windows XP 以降では、ドライバー検証マネージャーは、さまざまな方法でオプションを選択できます。

-   オプションがアクティブな完全に制御するには、選択、**カスタム設定を作成**タスクとキーを押して**次**します。 次の画面では、次のように選択します。**完全な一覧から個々 の設定を選択します。**、キーを押します**次**。 次の画面では、Driver Verifier のオプション (特別なプール、プールの追跡、強制 IRQL 検査、I/O の検証、強化された I/O の検証、デッドロックの検出、DMA の検証と低リソース シミュレーション--および Windows でディスクの整合性チェックをすべて一覧表示されます。Server 2003 以降)。 以降 Windows Vista では、オプションはそのも含める[セキュリティ チェック](security-checks.md)と[その他のチェック](miscellaneous-checks.md)。 Windows 8 以降では、オプションはそのも含める[Power Framework 遅延ファジー テスト](concurrency-stress-test.md)、 [DDI 準拠の検査](ddi-compliance-checking.md)、[不変な Mdl のスタック](invariant-mdl-checking-for-stack.md)、および[不変な Mdl のドライバーの](invariant-mdl-checking-for-driver.md)します。 Windows 8.1 以降のオプションも含まれます[NDIS/WIFI 検証](ndis-wifi-verification.md)、[カーネル同期遅延ファジー テスト](kernel-synchronization-delay-fuzzing.md)、 [VM switch 検証](vm-switch-verification.md)、および[体系的な低リソース シミュレーション](systematic-low-resource-simulation.md)します。 どのオプションを使用すると、アクティブ化を確認します。

-   オプションの定義済みセットから選択するには、選択、**カスタム設定を作成**タスクとキーを押して**次**します。 次の画面では、次のように選択します。**定義済みの設定を有効にする**チェック ボックスのいずれかを選択します。 選択すると、**標準設定**により、特別なプール、強制 IRQL 検査、プールの追跡、I/O の検証、DMA の検証、およびデッドロックを検出します。 有効でオプション標準を選択すると Windows Vista 以降、[セキュリティ チェック](security-checks.md)と[その他のチェック](miscellaneous-checks.md)。 有効でオプション標準を選択すると Windows 8 以降、 [DDI 準拠の検査](ddi-compliance-checking.md)します。 選択すると、**低リソース シミュレーション**チェック ボックスは、低リソース シミュレーションを使用できます。 選択すると、 **I/O の検証の強化された**チェック ボックスが強化された I/O の検証を使用します。 Windows Server 2003 以降では、次のように選択すると、**ディスクの整合性チェック**チェック ボックスは、ディスクの整合性チェックを使用します。

-   標準のオプションを選択する場合、**標準設定を作成する**タスク。 標準の設定には、特別なプール、強制 IRQL 検査、プールの追跡、I/O の検証、DMA の検証、およびデッドロック検出が含まれます。 Windows Vista 以降、標準の設定にはまた、[セキュリティ チェック](security-checks.md)と[(その他) を確認します](miscellaneous-checks.md)。 Windows 8 以降、標準の設定はそのも含める[DDI 準拠の検査](ddi-compliance-checking.md)します。

場合は、Windows vista では、開始することに注意してください、**低リソース シミュレーション**上に示した最初の 2 つのメソッドのいずれかのチェック ボックスを選択すると、次の画面は、確率、アプリケーション、プールのタグを設定するための画面と低リソース シミュレーションのシステム時刻の遅延起動オプションです。 これらのオプションを目的の値に設定します。

いずれかの手順を実行したときにキーを押して**次**します。 参照してください[検証するドライバーを選択すると](selecting-drivers-to-be-verified.md)の次の手順。

すべてのオプションを非アクティブ化し、検証済みのドライバーの一覧をクリア、選択、**既存の設定を削除**タスク。 キーを押します**完了**します。

### <a name="span-idrebootrequiredspanspan-idrebootrequiredspanreboot-required"></a><span id="reboot_required"></span><span id="REBOOT_REQUIRED"></span>再起動が必要です。

Windows vista 以降では、アクティブ化し、(「再起動」) を再起動しなくても、すべてのオプションを非アクティブ化以外のコンピューター [DDI 準拠の検査](ddi-compliance-checking.md)、 [Power Framework 遅延ファジー テスト](concurrency-stress-test.md)、 [Storport 検証](dv-storport-verification.md)、または[SCSI 検証](scsi-verification.md)です。 詳細については、次を参照してください。[揮発性の設定を使用する](using-volatile-settings.md)します。

Windows Vista より前のシステムでは、アクティブ化しを再起動しなくても、特定のオプションを非アクティブ化することができますが、少なくとも 1 つのドライバーが、コンピューターを再起動してドライバーの検証を有効にした後にのみです。 詳細については、次を参照してください。[揮発性の設定を使用する](using-volatile-settings.md)します。

 

 





