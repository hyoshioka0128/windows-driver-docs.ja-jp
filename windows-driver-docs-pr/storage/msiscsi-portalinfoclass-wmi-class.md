---
title: MSiSCSI\_PortalInfoClass WMI クラス
description: MSiSCSI\_PortalInfoClass WMI クラス
ms.assetid: f22c36a9-28be-4de1-9e80-0f0c1bd6473d
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1dcd9aa016d09c1d7b4d86ca732966a300468983
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387453"
---
# <a name="msiscsiportalinfoclass-wmi-class"></a>MSiSCSI\_PortalInfoClass WMI クラス


## <span id="ddk_msiscsi_portalinfoclass_wmi_class_kr"></span><span id="DDK_MSISCSI_PORTALINFOCLASS_WMI_CLASS_KR"></span>


MSiSCSI\_PortalInfoClass WMI クラスは、iSCSI ポータルのコレクションに関する情報を公開します。

このクラスは、記憶域ミニポート ドライバーの特定のインスタンスに関連付けられているため、ミニポート ドライバーは、ミニポート ドライバーを管理する特定の物理デバイス オブジェクト (PDO) の名前を使用して、クラスを登録する必要があります。

MSiSCSI\_PortalInfoClass クラスで定義されます*Mgmt.mof*します。

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

WMI ツールのスイートでは、上記のクラス定義をコンパイルするときに生成、 [ **MSiSCSI\_PortalInfoClass** ](https://msdn.microsoft.com/library/windows/hardware/ff563097)データ構造体。

 

 





