---
title: 既定の規則セット (KMDF)
description: 既定の規則セット (Default.sdv) では、推奨される一連のドライバーを分析するときに使用する規則を指定します。
ms.assetid: A86161C6-52E8-457B-9C75-100D36796183
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 39b2fe9d94858baa577b994770872b35ea15b9ed
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371406"
---
# <a name="default-rule-set-kmdf"></a>既定の規則セット (KMDF)


既定の規則セット (Default.sdv) では、推奨される一連のドライバーを分析するときに使用する規則を指定します。

[DDI 使用量のルール設定 (KMDF)](ddi-usage-rule-set--kmdf-.md)
[IrpProcessing ルール設定 (KMDF)](irpprocessing-rule-set--kmdf-.md)
[Irql ルール設定 (KMDF)](irql-rule-set--kmdf-.md)
[ロック ルール設定 (KMDF)](locking-rule-set--kmdf-.md) 
[その他のルール設定 (KMDF)](miscellaneous-rule-set--kmdf-.md)
[RequestProcessing ルール設定 (KMDF)](requestprocessing-rule-set--kmdf-.md)
[Usb ルール設定 (KMDF)](usb-rule-set--kmdf-.md) 
**既定の規則を選択するには**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

2.  をクリックして、**ルール**タブ。**規則セット**、**既定**。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **Default.sdv**で、 **/check**オプション。 次に、例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:Default.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、次を参照してください。[ドライバーで障害を検出する Static Driver Verifier を使用して](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)と[Static Driver Verifier のコマンド (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)します。

 

 





