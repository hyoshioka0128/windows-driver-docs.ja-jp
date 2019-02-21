---
title: MS\_SM\_TargetInformationMethods WMI クラス
description: MS\_SM\_TargetInformationMethods WMI クラス
ms.assetid: faedf8cf-d69f-4a4c-bc32-fd6df102d027
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bd96c34c5371473a99e4630594ff4cbdc27647a2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529074"
---
# <a name="mssmtargetinformationmethods-wmi-class"></a>MS\_SM\_TargetInformationMethods WMI クラス


WMI クライアントが、MS を使用して\_SM\_TargetInformationMethods WMI クラスは、ファイバー チャネル プロトコル (FCP) についての HBA ミニポート ドライバーにクエリを実行します。 FCP の HBA ミニポート ドライバーが T11 委員会の FCP 情報関数についてのセクションで定義されている*ファイバー チャネル HBA API*仕様。 この WMI クラスには、データ ブロックがありません。 そのため、WMI ツールのスイートには、クラスに属するメソッドのパラメーター データを格納する構造が生成されますが、クラス自体に対応する構造を生成しません。

このクラスに属している各メソッドの MOF 構文は、メソッドのリファレンス ページの説明です。 次のトピックでは、これらのメソッドとそれらに付随する構造体について説明します。

[**SM\_GetTargetMapping**](sm-gettargetmapping.md)

[**SM\_GetBindingCapability**](sm-getbindingcapability.md)

[**SM\_GetBindingSupport**](sm-getbindingsupport.md)

[**SM\_SetBindingSupport**](sm-setbindingsupport.md)

[**SM\_GetPersistentBinding**](sm-getpersistentbinding.md)

[**SM\_SetPersistentBinding**](sm-setpersistentbinding.md)

[**SM\_RemovePersistentBinding**](sm-removepersistentbinding.md)

[**SM\_GetLUNStatistics**](sm-getlunstatistics.md)

MS\_SM\_TargetInformationMethods クラスが次のように定義されている*Hbaapi.mof*:

```cpp
class MS_SM_TargetInformationMethods
{
    [key]
    string  InstanceName;
    boolean Active;

    [Implemented, WmiMethodId(1)]
    void SM_GetTargetMapping(
                [in, HBAType("HBA_WWN")] uint8  HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DomainPortWWN[8],
                [in ]
                 uint32 InEntryCount,
                [out, HBA_STATUS_QUALIFIERS]
                 HBA_STATUS HBAStatus,
                [out] 
                 uint32 TotalEntryCount,
                [out] 
                 uint32 OutEntryCount,
                [out, WmiSizeIs("OutEntryCount")]
                 MS_SMHBA_SCSIENTRY Entry[]
                );

    [Implemented, WmiMethodId(2)]
    void SM_GetBindingCapability(
                [in, HBAType("HBA_WWN")] uint8  HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DomainPortWWN[8],
                [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus,
                [out, HBAType("SMHBA_BIND_CAPABILITY")] uint32 Flags
                );

    [Implemented, WmiMethodId(3)]
    void SM_GetBindingSupport(
                [in, HBAType("HBA_WWN")] uint8  HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DomainPortWWN[8],
                [out, HBA_STATUS_QUALIFIERS]
                 HBA_STATUS HBAStatus,
                [out, HBAType("SMHBA_BIND_CAPABILITY")]
                 uint32 Flags
                );

    [Implemented, WmiMethodId(4)]
    void SM_SetBindingSupport(
                [in, HBAType("HBA_WWN")] uint8  HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DomainPortWWN[8],
                [in, HBAType("SMHBA_BIND_CAPABILITY")]
                 uint32 Flags,
                [out, HBA_STATUS_QUALIFIERS]
                 HBA_STATUS HBAStatus
                );

    [Implemented, WmiMethodId(5)]
    void SM_GetPersistentBinding(
                [in, HBAType("HBA_WWN")] uint8  HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DomainPortWWN[8],
                [in ]
                 uint32 InEntryCount,
                [out, HBA_STATUS_QUALIFIERS]
                 HBA_STATUS HBAStatus,
                [out]
                 uint32 TotalEntryCount,
                [out]
                 uint32 OutEntryCount,
                [out, WmiSizeIs("OutEntryCount")]
                 MS_SMHBA_BINDINGENTRY Entry[]
                );

    [Implemented, WmiMethodId(6)]
    void SM_SetPersistentBinding(
                [in, HBAType("HBA_WWN")] uint8  HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DomainPortWWN[8],
                [in ] uint32 InEntryCount,
                [in, WmiSizeIs("InEntryCount")]
                 MS_SMHBA_BINDINGENTRY Entry[],
                [out, HBA_STATUS_QUALIFIERS]
                 HBA_STATUS HBAStatus,
                [out ] uint32 OutStatusCount,
                [out, WmiSizeIs("OutStatusCount")]
                 HBA_STATUS EntryStatus[]
                );

    [Implemented, WmiMethodId(7)]
    void SM_RemovePersistentBinding(
                [in, HBAType("HBA_WWN")] uint8  HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DomainPortWWN[8],
                [in ]
                 uint32 EntryCount,
                [in, WmiSizeIs("EntryCount")]
                 MS_SMHBA_BINDINGENTRY Entry[],
                [out, HBA_STATUS_QUALIFIERS]
                 HBA_STATUS HBAStatus
                );

    [Implemented, WmiMethodId(8)]
    void SM_GetLUNStatistics(
                [in, HBAType("HBA_SCSIID")]
                 HBAScsiID Lunit,
                [out, HBA_STATUS_QUALIFIERS ]
                 HBA_STATUS HBAStatus,
                [out, HBAType("MS_SMHBA_PROTOCOLSTATISTICS") ]
                 MS_SMHBA_PROTOCOLSTATISTICS ProtocolStatistics
                );
};
```

 

 





