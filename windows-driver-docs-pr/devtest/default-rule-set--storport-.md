---
title: 既定の規則セット (Storport)
description: 既定の規則セット (Default.sdv) では、推奨される一連のドライバーを分析するときに使用する規則を指定します。
ms.assetid: 8310E393-4CA7-4701-8BBC-6E758C927FBE
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: d5c7f94469073467a95080ba1221e3320eac17de
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570312"
---
# <a name="default-rule-set-storport"></a>既定の規則セット (Storport)


既定の規則セット (Default.sdv) では、推奨される一連のドライバーを分析するときに使用する規則を指定します。

[DDI 使用量のルール設定 (Storport)](ddi-usage-rule-set--storport-.md)
[Irql ルール設定 (Storport)](irql-rule-set--storport-.md)
[ロック ルール設定 (Storport)](locking-rule-set--storport-.md)
[SrbProcessing ルール設定 (Storport)](srbprocessing-rule-set--storport-.md)
[VirtualStorport ルール設定 (Storport)](virtualstorport-rule-set--storport-.md)
**既定の規則を選択するには**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

2.  をクリックして、**ルール**タブ。**規則セット**、**既定**。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **Default.sdv**で、 **/check**オプション。 例:

    ```
    msbuild /t:sdv /p:Inputs="/check:Default.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、次を参照してください。[ドライバーで障害を検出する Static Driver Verifier を使用して](https://msdn.microsoft.com/library/windows/hardware/hh454281)と[Static Driver Verifier のコマンド (MSBuild)](https://msdn.microsoft.com/library/windows/hardware/hh466459)します。

 

 





