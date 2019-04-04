---
title: 既定のルール設定 (WDM)
description: 既定の規則セット (Default.sdv) では、推奨される一連のドライバーを分析するときに使用する規則を指定します。
ms.assetid: F03BEEDE-ED6E-4202-9FF5-74A098702E12
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 37a9a812f9cd7edfce41593a45d2843cc5437726
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529778"
---
# <a name="default-rule-set-wdm"></a>既定のルール設定 (WDM)


既定の規則セット (Default.sdv) では、推奨される一連のドライバーを分析するときに使用する規則を指定します。

[DDI 使用量のルール設定 (WDM)](ddi-usage-rule-set--wdm-.md)
[IrpProcessing ルール設定 (WDM)](irpprocessing-rule-set--wdm-.md)
[IrpTracking ルール設定 (WDM)](irptracking-rule-set--wdm-.md)
[Irql ルール設定 (WDM)](irql-rule-set--wdm-.md) 
 [LocalIrpProcessing ルール設定 (WDM)](localirpprocessing-rule-set--wdm-.md)
[ロック ルール設定 (WDM)](locking-rule-set--wdm-.md)
[その他のルール設定 (WDM)](miscellaneous-rule-set--wdm-.md)
[IrpPending ルール設定 (WDM)](irppending-rule-set--wdm-.md)
**既定の規則を選択するには**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

2.  をクリックして、**ルール**タブ。**規則セット**、**既定**。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **Default.sdv**で、 **/check**オプション。 次に、例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:Default.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、[ドライバーで障害を検出する Static Driver Verifier を使用して](https://msdn.microsoft.com/library/windows/hardware/hh454281)と[Static Driver Verifier のコマンド (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)を参照してください。

 

 





