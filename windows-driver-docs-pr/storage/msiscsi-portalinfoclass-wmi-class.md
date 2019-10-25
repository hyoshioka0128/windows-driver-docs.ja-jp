---
title: MSiSCSI\_PortalInfoClass WMI クラス
description: MSiSCSI\_PortalInfoClass WMI クラス
ms.assetid: f22c36a9-28be-4de1-9e80-0f0c1bd6473d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9381595afb06dbc2304cdcfab87b2fc03409bcbc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845335"
---
# <a name="msiscsi_portalinfoclass-wmi-class"></a>MSiSCSI\_PortalInfoClass WMI クラス


## <span id="ddk_msiscsi_portalinfoclass_wmi_class_kr"></span><span id="DDK_MSISCSI_PORTALINFOCLASS_WMI_CLASS_KR"></span>


MSiSCSI\_PortalInfoClass WMI クラスは、iSCSI ポータルのコレクションに関する情報を公開します。

このクラスは記憶域ミニポートドライバーの特定のインスタンスに関連付けられているため、ミニポートドライバーは、ミニポートドライバーが管理する特定の物理デバイスオブジェクト (PDO) の名前を使用してクラスを登録する必要があります。

MSiSCSI\_PortalInfoClass クラスは、*管理 .mof*で定義されています。

```cpp
class MSiSCSI_PortalInfoClass {
  [read,key] String  InstanceName;
  [read] boolean  Active;
  [WmiDataId(1), read, DisplayName("Count of Elements in
    iScsiPortalInfo array") : amended,
    cpp_quote(
    "\n    // Number of elements in  iScsiPortalInfo
    array\n"),
    Description("Number of elements in iScsiPortalInfo
    array") : amended] 
    uint32  PortalInfoCount;
  [WmiDataId(2), read, DisplayName("List Of Portals") :
    amended, Description("Variable length array of
    iScsiPortalInfo. PortalInfoCount specifies the 
    number of elements in the array") : amended,
    WmiSizeIs("PortalInfoCount")] 
    ISCSI_PortalInfo  PortalInformation[];
};
```

WMI ツールスイートは、前のクラス定義をコンパイルするときに、 [**Msiscsi\_PortalInfoClass**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsimgt/ns-iscsimgt-_msiscsi_portalinfoclass)データ構造体を生成します。

 

 





