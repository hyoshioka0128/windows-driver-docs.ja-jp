---
title: 15 ~ 20 のリセット (突然の削除する) 手順
description: 手順 15 から 20 までが、リセット (突然の削除) の手順を以下に示します。 手順は、UE ハングの検出と回復のフローの図に対応します。
ms.assetid: E72714A9-9B06-4609-820C-F25DC6BC0696
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c088a442c80dde3ff8ddda872eac39e855c7af8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549116"
---
# <a name="reset-surprise-remove-steps-15-20"></a>(突然の削除) のリセット: 15 ~ 20 のステップ


手順 15 から 20 までが、リセット (突然の削除) の手順を以下に示します。 手順は、図に示すように対応[UE ハングアップ検出と復旧フロー](wdi-ue-hang-detection-and-recovery-flow.md)します。

リセット回復を続行すると、バスにより PnP に突然削除 IRP を生成します。 NDIS が突然削除 IRP を受信すると、コールバックします WDI 突然削除 PnP イベントのコールバック。 WDI、LE がハングした WDI コマンドを返します、LE、WDI コマンドとして突然削除に転送します。 フローの残りの部分は、バス (USB など) で、実際のデバイス突然削除と同じです。

クリーンアップのコマンドは、リソースの戻り値を容易に LE に並べられます。 この状態で、LE をハードウェアは触れないでください。

| 手順 | アクション                                                                                                                                                               |
|------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 15   | NDIS コールバック、PnP イベントの突然削除します。                                                                                                                   |
| 16   | WDI コールバック、LE を突然削除します。                                                                                                                           |
| 17   | LE、ハングした WDI コマンドを返します。 WDI は診断と中止を除く、LE、WDI コマンドをシリアル化するため、LE には未処理の WDI コマンドのスロットのみ必要があります。 |
| 18   | 元の NDIS コマンドが返されたために、WDI はハングした WDI コマンドの戻り値を無視します。                                                                    |
| 19   | LE、WDI 驚きと削除 を返します。                                                                                                                                  |
| 20   | WDI 返します NDIS PnP 突然削除のコールバック。                                                                                                                  |

 

## <a name="related-topics"></a>関連トピック


[UE ハング検出: 1 ~ 14 のステップ](wdi-ue-hang-detection--step-1-to-step-14.md)

[UE ハングアップ検出と復旧フロー](wdi-ue-hang-detection-and-recovery-flow.md)

 

 






