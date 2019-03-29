---
title: 既定の規則セット (KMDF)
description: 既定の規則セット (Default.sdv) では、推奨される一連のドライバーを分析するときに使用する規則を指定します。
ms.assetid: A86161C6-52E8-457B-9C75-100D36796183
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: bf5ab6bb7dc2d41a6c996fda809331f9b6c7a278
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581121"
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

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **Default.sdv**で、 **/check**オプション。 例:

    ```
    msbuild /t:sdv /p:Inputs="/check:Default.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、次を参照してください。[ドライバーで障害を検出する Static Driver Verifier を使用して](https://msdn.microsoft.com/library/windows/hardware/hh454281)と[Static Driver Verifier のコマンド (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)します。

 

 





