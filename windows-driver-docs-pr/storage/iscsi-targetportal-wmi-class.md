---
title: ISCSI\_TargetPortal WMI クラス
description: ISCSI\_TargetPortal WMI クラス
ms.assetid: b163b2e7-8f12-4cd2-a682-7b755f28792e
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c093c046615a6849309a77a43bdf5f572799cd60
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841621"
---
# <a name="iscsi_targetportal-wmi-class"></a>ISCSI\_TargetPortal WMI クラス


## <span id="ddk_iscsi_targetportal_wmi_class_kr"></span><span id="DDK_ISCSI_TARGETPORTAL_WMI_CLASS_KR"></span>


ISCSI\_TargetPortal クラスは、ターゲットポータルを定義します。 この定義には、ソケット番号と、イニシエーターとターゲットが使用する IP プロトコルのバージョンに依存しない IP アドレスが含まれます。

このクラスは、*一般的な .mof*で次のように定義されています。

```cpp
class ISCSI_TargetPortal {
  [WmiDataId(1), Description("Network Address") : amended]
    ISCSI_IP_Address  Address;
  [WmiDataId(2), Description("Socket number") : amended]
    uint16 Socket;
};
```

WMI ツールスイートは、前のクラス定義をコンパイルするときに、 [**ISCSI\_TargetPortal**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsidef/ns-iscsidef-_iscsi_targetportal)データ構造を生成します。

 

 





