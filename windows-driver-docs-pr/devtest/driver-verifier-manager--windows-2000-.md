---
title: ドライバー検証マネージャー (Windows 2000)
description: ドライバー検証マネージャー (Windows 2000)
ms.assetid: d1266d2d-2388-472d-a1c4-875ed24913d4
keywords:
- ドライバー検証マネージャー
- 検証ユーティリティ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f7c17054c0b4065eaa72cc4f2c889217a6127d3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529795"
---
# <a name="driver-verifier-manager-windows-2000"></a>ドライバー検証マネージャー (Windows 2000)


## <span id="ddk_driver_verifier_manager_windows_2000__tools"></span><span id="DDK_DRIVER_VERIFIER_MANAGER_WINDOWS_2000__TOOLS"></span>


Windows 2000 バージョンのドライバー検証マネージャーでは、5 つの個別のパネルがあります。

1.  **ドライバ ステータスの**画面を表示すると、ドライバーが読み込まれ、検証し、Driver Verifier のオプションがアクティブです。 参照してください[ドライバー検証ツールの設定を表示する](viewing-driver-verifier-settings.md)詳細についてはします。

2.  **グローバル カウンター**画面には、Driver Verifier のアクションに関連する統計情報が表示されます。 これらの統計情報の一部は、特定の Driver Verifier のオプションに関連する、ですが、オプションがアクティブに関係なくこれらの統計情報が表示されます。 参照してください[グローバル カウンターの監視](monitoring-global-counters.md)詳細についてはします。

3.  **プール追跡**画面は、プールの割り当てに関する情報を表示します。 参照してください[カウンターを個別に監視](monitoring-individual-counters.md)詳細についてはします。

4.  **設定**画面がアクティブ化して、Driver Verifier のアクションを構成するために使用します。 この画面から加えられた変更は、[次へ] の起動後にも反映されます。 参照してください[ドライバー検証ツールのオプションの選択](selecting-driver-verifier-options.md)と[検証するドライバーを選択すると](selecting-drivers-to-be-verified.md)詳細についてはします。

5.  **揮発性の設定**Driver Verifier の揮発性のアクションを変更する画面を使用します。 この画面から加えられた変更は、すぐに反映します。 参照してください[揮発性の設定を使用する](using-volatile-settings.md)詳細についてはします。

いくつかの画面が、**更新頻度**にセクション。 これは、その画面に表示される情報が更新される頻度を制御に使用されます。 **低**、 **Medium**、および**高**画面ごとの 1 つ、5、または 10 秒をそれぞれ更新 Driver Verifier に指示します。 **手動**自動更新を無効にします。 **今すぐ更新**と、すぐに更新する画面のボタンをクリックします。

ドライバー検証マネージャーを終了するには、使用、**終了**ボタンをクリックします。 すべての変更を行ったし、対応するが押されていないかどうか**適用**ボタンを求められます、変更を保存するかどうか。

 

 





