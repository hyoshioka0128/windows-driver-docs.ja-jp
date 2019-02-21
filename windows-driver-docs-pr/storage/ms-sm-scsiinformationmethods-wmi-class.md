---
title: MS\_SM\_ScsiInformationMethods WMI クラス
description: MS\_SM\_ScsiInformationMethods WMI クラス
ms.assetid: 13e70e48-5364-4a63-8a83-d5ac02c8d17f
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: eb0b83b622bdd965adb9e0cecd72ee72dae959f5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551862"
---
# <a name="mssmscsiinformationmethods-wmi-class"></a>MS\_SM\_ScsiInformationMethods WMI クラス


記憶域管理 API をサポートする HBA ミニポート ドライバーは、MS を使用して\_SM\_ScsiInformationMethods WMI クラスの SCSI コマンドを送信します。 この WMI クラスには、データ ブロックがありません。 そのため、WMI ツールのスイートには、クラスに属するメソッドのパラメーター データを格納する構造が生成されますが、クラス自体に対応する構造を生成しません。

このクラスに属している各メソッドの MOF 構文は、メソッドのリファレンス ページの説明です。 次のトピックでは、これらのメソッドとそれらに付随する構造体について説明します。

[**SM\_ScsiInquiry**](sm-scsiinquiry.md)

[**SM\_ScsiReportLuns**](sm-scsireportluns.md)

[**SM\_ScsiReadCapacity**](sm-scsireadcapacity.md)

MS\_SM\_ScsiInformationMethods クラスが次のように定義されている*Hbaapi.mof*:

```cpp
class MS_SM_ScsiInformationMethods
{
    [key]
    string  InstanceName;
    boolean Active;

    [Implemented, WmiMethodId(1)]
    void SM_ScsiInquiry(
                [in, HBAType("HBA_WWN")] uint8  HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DiscoveredPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DomainPortWWN[8],
                [in, HBAType("HBA_SCSILUN")]
                 uint64 SmhbaLUN,
                [in ]
                 uint8  Cdb[6],
                [in ]
                 uint32 InRespBufferMaxSize,
                [in ]
                 uint32 InSenseBufferMaxSize,
                [out, HBA_STATUS_QUALIFIERS ]
                 HBA_STATUS HBAStatus,
                [out]
                 uint8  ScsiStatus,
                [out]
                 uint32 OutRespBufferSize,
                [out]
                 uint32 OutSenseBufferSize,
                [out, WmiSizeIs("OutRespBufferSize") ]
                 uint8 RespBuffer[],
                [out, WmiSizeIs("OutSenseBufferSize") ]
                 uint8 SenseBuffer[]
                );

    [Implemented, WmiMethodId(2)]
    void SM_ScsiReportLuns(
                [in, HBAType("HBA_WWN")] uint8  HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DiscoveredPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DomainPortWWN[8],
                [in ]
                 uint8  Cdb[12],
                [in ]
                 uint32 InRespBufferMaxSize,
                [in ]
                 uint32 InSenseBufferMaxSize,
                [out, HBA_STATUS_QUALIFIERS ]
                 HBA_STATUS HBAStatus,
                [out]
                 uint8  ScsiStatus,
                [out]
                 uint32 TotalRespBufferSize,
                [out]
                 uint32 OutRespBufferSize,
                [out]
                 uint32 OutSenseBufferSize,
                [out, WmiSizeIs("OutRespBufferSize") ]
                 uint8 RespBuffer[],
                [out, WmiSizeIs("OutSenseBufferSize") ]
                 uint8 SenseBuffer[]
                );
 
    [Implemented, WmiMethodId(3)]
    void SM_ScsiReadCapacity(
                [in, HBAType("HBA_WWN")] uint8  HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DiscoveredPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DomainPortWWN[8],
                [in, HBAType("HBA_SCSILUN")]
                 uint64 SmhbaLUN,
                [in ]
                 uint8  Cdb[16],
                [in ]
                 uint32 InRespBufferMaxSize,
                [in ]
                 uint32 InSenseBufferMaxSize,
                [out, HBA_STATUS_QUALIFIERS ]
                 HBA_STATUS HBAStatus,
                [out]
                 uint8  ScsiStatus,
                [out]
                 uint32 OutRespBufferSize,
                [out]
                 uint32 OutSenseBufferSize,
                [out, WmiSizeIs("OutRespBufferSize") ]
                 uint8  RespBuffer[],
                [out, WmiSizeIs("OutSenseBufferSize") ]
                 uint8  SenseBuffer[]
                );
};
```

 

 





