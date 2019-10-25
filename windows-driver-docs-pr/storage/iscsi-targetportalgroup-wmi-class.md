---
title: ISCSI\_TargetPortalGroup WMI クラス
description: ISCSI\_TargetPortalGroup WMI クラス
ms.assetid: dff17d52-b308-49cc-97ec-d54eddb4e747
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5671cf4e1f7435b3c4e156ee3e4f7d27dfbe5732
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841618"
---
# <a name="iscsi_targetportalgroup-wmi-class"></a>ISCSI\_TargetPortalGroup WMI クラス


## <span id="ddk_iscsi_targetportalgroup_wmi_class_kr"></span><span id="DDK_ISCSI_TARGETPORTALGROUP_WMI_CLASS_KR"></span>


ISCSI\_TargetPortalGroup クラスは、ターゲットポータルグループを定義します。

このクラスは、*一般的な .mof*で次のように定義されています。

```cpp
class ISCSI_TargetPortalGroup {
  [WmiDataId(1), description("Number of portals in group") :
    amended]
    uint32  PortalCount;
  [WmiDataId(2), WmiSizeIs("PortalCount"),
    description("Target portals in group") : amended]
    ISCSI_TargetPortal  Portals[];
};
```

WMI ツールスイートは、前のクラス定義をコンパイルするときに、 [**ISCSI\_TargetPortalGroup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsidef/ns-iscsidef-_iscsi_targetportalgroup)データ構造を生成します。

 

 





