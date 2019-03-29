---
title: ソフトウェアのレジストリ設定の追加
description: ソフトウェアのレジストリ設定の追加
ms.assetid: 96c7fc9e-885c-43ec-973a-6e6d984fe7d0
keywords:
- INF ファイル WDK の表示、ソフトウェアのレジストリ設定
- ソフトウェアのレジストリ設定 WDK の表示
- レジストリ WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f02512d274d0cffe5d84a30ec396253977b88df8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581439"
---
# <a name="adding-software-registry-settings"></a>ソフトウェアのレジストリ設定の追加


INF ファイルする必要がありますすべてソフトウェア レジストリ設定を追加、プラグ アンド プレイ (PnP) に次の例に示すようにソフトウェア キー。

```inf
[Xxx.Mfg]
"RADEON 8500/RADEON 8500LE (R200 LDDM)" = R200_R200, PCI\VEN_1002&DEV_514c&SUBSYS_003a1002

[R200_R200]
Include=msdv.inf
CopyFiles=R200.Miniport, R200.Display
AddReg = R200_SoftwareDeviceSettings
AddReg = R200_R200_SoftwareDeviceSettings
DelReg = R200_RemoveDeviceSettings 
```

 

 





