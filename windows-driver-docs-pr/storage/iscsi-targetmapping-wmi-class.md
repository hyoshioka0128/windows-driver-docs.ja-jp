---
title: ISCSI\_TargetMapping WMI クラス
description: ISCSI\_TargetMapping WMI クラス
ms.assetid: b2c4634a-852b-471a-8764-025780e36c0f
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 70477f5fd6992813b7796db21b0b56db2be70e95
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557506"
---
# <a name="iscsitargetmapping-wmi-class"></a>ISCSI\_TargetMapping WMI クラス


## <span id="ddk_iscsi_targetmapping_wmi_class_kr"></span><span id="DDK_ISCSI_TARGETMAPPING_WMI_CLASS_KR"></span>


ISCSI\_TargetMapping WMI クラスは、64 ビット iSCSI Lun のグループにイニシエーターのホスト システムでローカルに定義されている論理ユニット番号 (Lun) のコレクションをマップします。 自体によって 64 ビット iSCSI LUN は、それが表す論理ユニットを一意に識別していません。 ただし、iSCSI LUN と論理ユニットが属している、ターゲットの名前は一意に識別、論理ユニットをネットワーク上の任意の場所。

管理アプリケーションは、ISCSI を使用できる\_TargetMapping WMI クラスがどのような Lun を割り当てるリモート論理ユニットをローカルで列挙されるときを指定します。

このクラスを定義するマッピングは、特定のターゲットのログオン セッションに関連付けられます。 [MSiSCSI\_TargetMappings WMI クラス](msiscsi-targetmappings-wmi-class.md)すべての特定のアダプター インスタンスに関連付けられているマッピングについて説明します。

このクラスが次のように定義されている*Common.mof*します。

```cpp
class ISCSI_TargetMapping {
  [WmiDataId(1), description("OS Scsi bus number target 
    is mapped to. If 0xffffffff then any value can be picked
    by the miniport.") : amended]
    uint32  OSBus;
  [WmiDataId(2), description("OS Scsi Target number target
    is mapped to. If 0xffffffff then any value can be picked
    by the miniport.") : amended]
    uint32  OSTarget;
  [WmiDataId(3), Description("Unique Session ID for the 
    target mapping") : amended] 
    uint64  UniqueSessionId;
  [WmiDataId(4), description("Count of LUNs mapped for this 
    target") : amended]
    uint32  LUNCount;
  [WmiDataId(5), MaxLen(MAX_ISCSI_NAME_LEN),
     description("Target Name") : amended]
    string  TargetName;
  [WmiDataId(6), Description("TRUE if session created from a
    persistent login") : amended]
    boolean  FromPersistentLogin;
  [WmiDataId(7), WmiSizeIs("LunCount"),
    description("List of LUNs mapped for this target") : 
    amended]
    ISCSI_LUNList  LUNList[];
};
```

 

 





