---
title: ISCSI\_TargetPortal WMI クラス
description: ISCSI\_TargetPortal WMI クラス
ms.assetid: b163b2e7-8f12-4cd2-a682-7b755f28792e
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f081ade43895a41dc5e8e5703f556e70dd762a99
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385389"
---
# <a name="iscsitargetportal-wmi-class"></a>ISCSI\_TargetPortal WMI クラス


## <span id="ddk_iscsi_targetportal_wmi_class_kr"></span><span id="DDK_ISCSI_TARGETPORTAL_WMI_CLASS_KR"></span>


ISCSI\_TargetPortal クラスは、ターゲット ポータルを定義します。 この定義には、ソケットの数と、イニシエーターとターゲットを使用する IP プロトコルのバージョンから独立している IP アドレスが含まれます。

このクラスが次のように定義されている*Common.mof*します。

```cpp
class ISCSI_TargetPortal {
  [WmiDataId(1), Description("Network Address") : amended]
    ISCSI_IP_Address  Address;
  [WmiDataId(2), Description("Socket number") : amended]
    uint16 Socket;
};
```

WMI ツールのスイートでは、上記のクラス定義をコンパイルするときに生成、 [ **ISCSI\_TargetPortal** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/iscsidef/ns-iscsidef-_iscsi_targetportal)データ構造体。

 

 





