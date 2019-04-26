---
title: MS\_SM\_FabricAndDomainManagementMethods WMI クラス
description: MS\_SM\_FabricAndDomainManagementMethods WMI クラス
ms.assetid: dfd6afd3-0a0c-4620-b961-2235a91d8b17
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b107d42bcf379c6d01f952ecd4105877d0ae19ca
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355197"
---
# <a name="mssmfabricanddomainmanagementmethods-wmi-class"></a>MS\_SM\_FabricAndDomainManagementMethods WMI クラス


記憶域管理 API をサポートする HBA ミニポート ドライバーは、MS を使用して\_SM\_FabricAndDomainManagementMethods WMI クラスを WMI クライアント ファイバー チャネルのサービスを提供します。 ファイバー チャネルのサービスが、T11 委員会によって定義されている*ファイバー チャネル HBA API*仕様。 この WMI クラスには、データ ブロックがありません。 そのため、WMI ツールのスイートには、クラスに属するメソッドのパラメーター データを格納する構造が生成されますが、クラス自体に対応する構造を生成しません。

このクラスに属している各メソッドの MOF 構文は、メソッドのリファレンス ページの説明です。 次のトピックでは、これらのメソッドとそれらに付随する構造体について説明します。

SM\_SendTEST

SM\_SendECHO

SM\_SendSMPPassThru

[**SM\_SendCTPassThru**](sm-sendctpassthru.md)

[**SM\_GetRNIDMgmtInfo**](sm-getrnidmgmtinfo.md)

[**SM\_SetRNIDMgmtInfo**](sm-setrnidmgmtinfo.md)

[**SM\_SendRNID**](sm-sendrnid.md)

[**SM\_SendRPL**](sm-sendrpl.md)

[**SM\_SendRPS**](sm-sendrps.md)

[**SM\_SendSRL**](sm-sendsrl.md)

[**SM\_SendLIRR**](sm-sendlirr.md)

[**SM\_SendRLS**](sm-sendrls.md)

MS\_SM\_FabricAndDomainManagementMethods クラスが次のように定義されている*Hbaapi.mof*:

```cpp
class MS_SM_FabricAndDomainManagementMethods
{
    [key]
    string  InstanceName;
    boolean Active;

// new FC specific

    [Implemented, WmiMethodId(1)]
    void SM_SendTEST(
                [in, HBAType("HBA_WWN")] uint8  HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DestWWN[8],
                [in ] uint32  DestFCID,
                [in ] uint32  ReqBufferSize,
                [in, WmiSizeIs("ReqBufferSize") ] uint8  ReqBuffer[],
                [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus
                );

// new FC specific

    [Implemented, WmiMethodId(2)]
    void SM_SendECHO(
                [in, HBAType("HBA_WWN")] uint8  HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DestWWN[8],
                [in ] uint32  DestFCID,
                [in ] uint32  InRespBufferMaxSize,
                [in ] uint32  ReqBufferSize,
                [in, WmiSizeIs("ReqBufferSize") ] uint8  ReqBuffer[],
                [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus,
                [out] uint32  OutRespBufferSize,
                [out, WmiSizeIs("OutRespBufferSize") ] uint8  RespBuffer[]
                );

// new SAS specific

    [Implemented, WmiMethodId(3)]
    void SM_SendSMPPassThru(
                [in, HBAType("HBA_WWN")] uint8  HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DestPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8  DomainPortWWN[8],
                [in ] uint32  InRespBufferMaxSize,
                [in ] uint32  ReqBufferSize,
                [in, WmiSizeIs("ReqBufferSize") ] uint8  ReqBuffer[],
                [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus,
                [out] uint32  TotalRespBufferSize,
                [out] uint32  OutRespBufferSize,
                [out, WmiSizeIs("OutRespBufferSize") ] uint8  RespBuffer[]
                );

// old FC specific

    [Implemented, WmiMethodId(10)]
    void SM_SendCTPassThru(
                [in, HBAType("HBA_WWN")] uint8  HbaPortWWN[8],
                [in ] uint32  InRespBufferMaxSize,
                [in ] uint32  ReqBufferSize,
                [in, WmiSizeIs("ReqBufferSize") ] uint8  ReqBuffer[],
                [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus,
                [out] uint32  TotalRespBufferSize,
                [out] uint32  OutRespBufferSize,
                [out, WmiSizeIs("OutRespBufferSize") ] uint8  RespBuffer[]
                );

// old FC specific

    [Implemented, WmiMethodId(11)]
    void SM_GetRNIDMgmtInfo(
                [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus,
                [out] HBAFC3MgmtInfo MgmtInfo
                );

// old FC specific

    [Implemented, WmiMethodId(12)]
    void SM_SetRNIDMgmtInfo(
                [in ] HBAFC3MgmtInfo MgmtInfo,
                [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus
                );

// old FC specific

    [Implemented, WmiMethodId(13)]
    void SM_SendRNID(
                [in, HBAType("HBA_WWN")] uint8 HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8 DestWWN[8],
                [in ] uint32  DestFCID,
                [in ] uint32  NodeIdDataFormat,
                [in ] uint32  InRespBufferMaxSize,
                [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus,
                [out] uint32  TotalRespBufferSize,
                [out] uint32  OutRespBufferSize,
                [out, WmiSizeIs("OutRespBufferSize")] uint8 RespBuffer[]
                );

// old FC specific

    [Implemented, WmiMethodId(14)]
    void SM_SendRPL(
                [in, HBAType("HBA_WWN")] uint8 HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8 AgentWWN[8],
                [in ] uint32  AgentDomain,
                [in ] uint32  PortIndex,
                [in ] uint32  InRespBufferMaxSize,
                [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus,
                [out] uint32  TotalRespBufferSize,
                [out] uint32  OutRespBufferSize,
                [out, WmiSizeIs("OutRespBufferSize")] uint8 RespBuffer[]
                );

// old FC specific

    [Implemented, WmiMethodId(15)]
    void SM_SendRPS(
                [in, HBAType("HBA_WWN")] uint8 HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8 AgentWWN[8],
                [in, HBAType("HBA_WWN")] uint8 ObjectWWN[8],
                [in ] uint32  AgentDomain,
                [in ] uint32  ObjectPortNumber,
                [in ] uint32  InRespBufferMaxSize,
                [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus,
                [out] uint32  TotalRespBufferSize,
                [out] uint32  OutRespBufferSize,
                [out, WmiSizeIs("OutRespBufferSize")] uint8 RespBuffer[]
                );

// old FC specific

    [Implemented, WmiMethodId(16)]
    void SM_SendSRL(
                [in, HBAType("HBA_WWN")] uint8 HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8 WWN[8],
                [in ] uint32  Domain,
                [in ] uint32  InRespBufferMaxSize,
                [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus,
                [out] uint32  TotalRespBufferSize,
                [out] uint32  OutRespBufferSize,
                [out, WmiSizeIs("OutRespBufferSize")] uint8 RespBuffer[]
                );

// old FC specific

    [Implemented, WmiMethodId(17)]
    void SM_SendLIRR(
                [in, HBAType("HBA_WWN")] uint8 SourceWWN[8],
                [in, HBAType("HBA_WWN")] uint8 DestWWN[8],
                [in ] uint8   Function,
                [in ] uint8   Type,
                [in ] uint32  InRespBufferMaxSize,
                [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus,
                [out] uint32  TotalRespBufferSize,
                [out] uint32  OutRespBufferSize,
                [out, WmiSizeIs("OutRespBufferSize")] uint8 RespBuffer[]
                );

// old FC specific

    [Implemented, WmiMethodId(18)]
    void SM_SendRLS(
                [in, HBAType("HBA_WWN")] uint8 HbaPortWWN[8],
                [in, HBAType("HBA_WWN")] uint8 DestWWN[8],
                [in ] uint32  InRespBufferMaxSize,
                [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus,
                [out] uint32  TotalRespBufferSize,
                [out] uint32  OutRespBufferSize,
                [out, WmiSizeIs("OutRespBufferSize")] uint8 RespBuffer[]
                );
};
```

 

 





