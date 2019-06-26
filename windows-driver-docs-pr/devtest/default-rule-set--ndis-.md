---
title: 既定の規則セット (NDIS)
description: 既定の規則セット (Default.sdv) では、推奨される一連のドライバーを分析するときに使用する規則を指定します。
ms.assetid: ED809122-5938-4087-AAB8-0D3EB6DB1092
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: e9f51542c76e8893c9652b15d51eb3c0ebddcba6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371535"
---
# <a name="default-rule-set-ndis"></a>既定の規則セット (NDIS)


既定の規則セット (Default.sdv) では、推奨される一連のドライバーを分析するときに使用する規則を指定します。

[DDI 使用量のルール設定 (NDIS)](ddi-usage-rule-set--ndis-.md)
[IRQL ルール設定 (NDIS)](irql-rule-set--ndis-.md)
[ロック ルール設定 (NDIS)](locking-rule-set--ndis-.md)
[メモリ使用量のルール設定 (NDIS)](memory-usage-rule-set--ndis-.md)
[その他のルール設定 (NDIS)](miscellaneous-rule-set--ndis-.md)
[OidProcessing ルール設定 (NDIS)](oidprocessing-rule-set--ndis-.md)
**既定の規則を選択するには**

1.  Microsoft Visual Studio で、ドライバーのプロジェクト (.vcxProj) を選択します。 **ドライバー**  メニューのをクリックして**Static Driver Verifier を起動しています**.

2.  をクリックして、**ルール**タブ。**規則セット**、**既定**。

    Visual Studio の開発者コマンド プロンプト ウィンドウから既定のルールを選択するには、次のように指定します。 **Default.sdv**で、 **/check**オプション。 次に、例を示します。

    ```
    msbuild /t:sdv /p:Inputs="/check:Default.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    詳細については、次を参照してください。[ドライバーで障害を検出する Static Driver Verifier を使用して](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)と[Static Driver Verifier のコマンド (MSBuild)](https://docs.microsoft.com/windows-hardware/drivers/devtest/-static-driver-verifier-commands--msbuild-)します。

 

 





