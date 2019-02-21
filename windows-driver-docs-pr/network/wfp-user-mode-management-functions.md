---
title: WFP ユーザー モードの管理機能
description: このトピックでは、WFP ユーザー モードの管理機能について説明します。
ms.assetid: 14accd49-5b96-40]()e6-b9d7-6638a4e5c2dc
keywords:
- WFP ユーザー モードの管理機能はネットワーク ドライバー
ms.date: 11/07/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8fd4d0cf0aa8818acd22c2a49553abd2d7fe99e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552945"
---
# <a name="wfp-user-mode-management-functions"></a>WFP ユーザー モードの管理機能

Windows フィルタ リング プラットフォームのユーザー モードの管理機能のセマンティクスはまったく同じから呼び出されるとコールアウト ドライバーとして、ユーザー モード アプリケーションから呼び出されたときに、戻り値の型がある点が、 **NTSTATUS**コードWin32 エラー コードではなく。 

これらの関数が記載されて、[管理機能](https://msdn.microsoft.com/library/windows/hardware/aa364943)ユーザー モードの[WFP 関数](https://msdn.microsoft.com/library/windows/hardware/aa364931)ドキュメント。 

> [!NOTE]
> 各関数のカーネル モード バージョンは、fwpmk.h で定義されます。 各関数のユーザー モード バージョンは、fwpmu.h で定義されます。
 
これらの関数を除くのすべての呼び出し元[FwpmFreeMemory0](https://msdn.microsoft.com/library/windows/hardware/aa364071) IRQL で実行する必要があります PASSIVE_LEVEL を = です。 呼び出し元**FwpmFreeMemory0** IRQL で実行する必要があります < = DISPATCH_LEVEL します。

## <a name="callout-management"></a>引き出し線の管理

- [FwpmCalloutAdd0](https://msdn.microsoft.com/library/windows/hardware/aa364010) 
- [FwpmCalloutCreateEnumHandle0](https://msdn.microsoft.com/library/windows/hardware/aa364012) 
- [FwpmCalloutDeleteById0](https://msdn.microsoft.com/library/windows/hardware/aa364013) 
- [FwpmCalloutDeleteByKey0](https://msdn.microsoft.com/library/windows/hardware/aa364016) 
- [FwpmCalloutDestroyEnumHandle0](https://msdn.microsoft.com/library/windows/hardware/aa364017) 
- [FwpmCalloutEnum0](https://msdn.microsoft.com/library/windows/hardware/aa364020) 
- [FwpmCalloutGetById0](https://msdn.microsoft.com/library/windows/hardware/aa364022) 
- [FwpmCalloutGetByKey0](https://msdn.microsoft.com/library/windows/hardware/aa364024) 
- [FwpmCalloutGetSecurityInfoByKey0](https://msdn.microsoft.com/library/windows/hardware/aa364026) 
- [FwpmCalloutSetSecurityInfoByKey0](https://msdn.microsoft.com/library/windows/hardware/aa364027) 

## <a name="connection-object-management"></a>接続オブジェクトの管理

- [FwpmConnectionCreateEnumHandle0](https://msdn.microsoft.com/library/windows/hardware/hh447303) 
- [FwpmConnectionDestroyEnumHandle0](https://msdn.microsoft.com/library/windows/hardware/hh447304) 
- [FwpmConnectionEnum0](https://msdn.microsoft.com/library/windows/hardware/hh447305) 
- [FwpmConnectionGetById0](https://msdn.microsoft.com/library/windows/hardware/hh447307) 
- [FwpmConnectionGetSecurityInfo0](https://msdn.microsoft.com/library/windows/hardware/hh447308) 
- [FwpmConnectionSetSecurityInfo0](https://msdn.microsoft.com/library/windows/hardware/hh447309) 

## <a name="event-management"></a>イベントの管理

- [FwpmNetEventCreateEnumHandle0](https://msdn.microsoft.com/library/windows/hardware/aa364175) 
- [FwpmNetEventDestroyEnumHandle0](https://msdn.microsoft.com/library/windows/hardware/aa364176) 
- FwpmNetEventEnum:
    - [FwpmNetEventEnum0](https://msdn.microsoft.com/library/windows/hardware/aa364177) (Windows Vista)
    - [FwpmNetEventEnum1](https://msdn.microsoft.com/library/windows/hardware/dd744936) (Windows 7)
    - [FwpmNetEventEnum2](https://msdn.microsoft.com/library/windows/hardware/hh447314) (Windows 8)
- [FwpmNetEventsGetSecurityInfo0](https://msdn.microsoft.com/library/windows/hardware/aa814094) 
- [FwpmNetEventsSetSecurityInfo0](https://msdn.microsoft.com/library/windows/hardware/aa814095) 

## <a name="filter-management"></a>フィルターの管理

- [FwpmFilterAdd0](https://msdn.microsoft.com/library/windows/hardware/aa364046) 
- [FwpmFilterCreateEnumHandle0](https://msdn.microsoft.com/library/windows/hardware/aa364048) 
- [FwpmFilterDeleteById0](https://msdn.microsoft.com/library/windows/hardware/aa364050) 
- [FwpmFilterDeleteByKey0](https://msdn.microsoft.com/library/windows/hardware/aa364053) 
- [FwpmFilterDestroyEnumHandle0](https://msdn.microsoft.com/library/windows/hardware/aa364055) 
- [FwpmFilterEnum0](https://msdn.microsoft.com/library/windows/hardware/aa364058) 
- [FwpmFilterGetById0](https://msdn.microsoft.com/library/windows/hardware/aa364059) 
- [FwpmFilterGetByKey0](https://msdn.microsoft.com/library/windows/hardware/aa364060) 
- [FwpmFilterGetSecurityInfoByKey0](https://msdn.microsoft.com/library/windows/hardware/aa364061) 
- [FwpmFilterSetSecurityInfoByKey0](https://msdn.microsoft.com/library/windows/hardware/aa364064) 

## <a name="layer-management"></a>レイヤーの管理

- [FwpmLayerCreateEnumHandle0](https://msdn.microsoft.com/library/windows/hardware/aa364167) 
- [FwpmLayerDestroyEnumHandle0](https://msdn.microsoft.com/library/windows/hardware/aa364168) 
- [FwpmLayerEnum0](https://msdn.microsoft.com/library/windows/hardware/aa364169) 
- [FwpmLayerGetById0](https://msdn.microsoft.com/library/windows/hardware/aa364170) 
- [FwpmLayerGetByKey0](https://msdn.microsoft.com/library/windows/hardware/aa364171) 
- [FwpmLayerGetSecurityInfoByKey0](https://msdn.microsoft.com/library/windows/hardware/aa364172) 
- [FwpmLayerSetSecurityInfoByKey0](https://msdn.microsoft.com/library/windows/hardware/aa364174) 

## <a name="provider-context-management"></a>プロバイダー コンテキストの管理

- [FwpmProviderContextAdd:
    - [FwpmProviderContextAdd0](https://msdn.microsoft.com/library/windows/hardware/aa364181) (Windows Vista)
    - [FwpmProviderContextAdd1](https://msdn.microsoft.com/library/windows/hardware/dd744940) (Windows 7)
    - [FwpmProviderContextAdd2](https://msdn.microsoft.com/library/windows/hardware/hh447316) (Windows 8)
- [FwpmProviderContextCreateEnumHandle0](https://msdn.microsoft.com/library/windows/hardware/aa364182) 
- [FwpmProviderContextDeleteById0](https://msdn.microsoft.com/library/windows/hardware/aa364183) 
- [FwpmProviderContextDeleteByKey0](https://msdn.microsoft.com/library/windows/hardware/aa364184) 
- [FwpmProviderContextDestroyEnumHandle0](https://msdn.microsoft.com/library/windows/hardware/aa364185) 
- FwpmProviderContextEnum:
    - [FwpmProviderContextEnum0](https://msdn.microsoft.com/library/windows/hardware/aa364186) (Windows Vista)
    - [FwpmProviderContextEnum1](https://msdn.microsoft.com/library/windows/hardware/dd744941) (Windows 7)
    - [FwpmProviderContextEnum2](https://msdn.microsoft.com/library/windows/hardware/hh447332) (Windows 8)
- FwpmProviderContextGetById:
    - [FwpmProviderContextGetById0](https://msdn.microsoft.com/library/windows/hardware/aa364187) (Windows Vista)
    - [FwpmProviderContextGetById1](https://msdn.microsoft.com/library/windows/hardware/dd744942) (Windows 7)
    - [FwpmProviderContextGetById2](https://msdn.microsoft.com/library/windows/hardware/hh447335) (Windows 8)
- FwpmProviderContextGetByKey:
    - [FwpmProviderContextGetByKey0](https://msdn.microsoft.com/library/windows/hardware/aa364188) (Windows Vista)
    - [FwpmProviderContextGetByKey1](https://msdn.microsoft.com/library/windows/hardware/dd744943) (Windows 7)
    - [FwpmProviderContextGetByKey2](https://msdn.microsoft.com/library/windows/hardware/hh447337) (Windows 8)
- [FwpmProviderContextGetSecurityInfoByKey0](https://msdn.microsoft.com/library/windows/hardware/aa364189) 
- [FwpmProviderContextSetSecurityInfoByKey0](https://msdn.microsoft.com/library/windows/hardware/aa364190) 

## <a name="provider-management"></a>プロバイダーの管理

- [FwpmProviderAdd0](https://msdn.microsoft.com/library/windows/hardware/aa364180) 
- [FwpmProviderCreateEnumHandle0](https://msdn.microsoft.com/library/windows/hardware/aa364194) 
- [FwpmProviderDeleteByKey0](https://msdn.microsoft.com/library/windows/hardware/aa364195) 
- [FwpmProviderDestroyEnumHandle0](https://msdn.microsoft.com/library/windows/hardware/aa364196) 
- [FwpmProviderEnum0](https://msdn.microsoft.com/library/windows/hardware/aa364197) 
- [FwpmProviderGetByKey0](https://msdn.microsoft.com/library/windows/hardware/aa364198) 
- [FwpmProviderGetSecurityInfoByKey0](https://msdn.microsoft.com/library/windows/hardware/aa364199) 
- [FwpmProviderSetSecurityInfoByKey0](https://msdn.microsoft.com/library/windows/hardware/aa364200) 

## <a name="session-management"></a>セッションの管理

- [FwpmEngineClose0](https://msdn.microsoft.com/library/windows/hardware/aa364034) 
- [FwpmEngineGetOption0](https://msdn.microsoft.com/library/windows/hardware/aa364035) 
- [FwpmEngineGetSecurityInfo0](https://msdn.microsoft.com/library/windows/hardware/aa364038) 
- [FwpmEngineOpen0](https://msdn.microsoft.com/library/windows/hardware/aa364040) 
- [FwpmEngineSetOption0](https://msdn.microsoft.com/library/windows/hardware/aa364042) 
- [FwpmEngineSetSecurityInfo0](https://msdn.microsoft.com/library/windows/hardware/aa364044) 
- [FwpmSessionCreateEnumHandle0](https://msdn.microsoft.com/library/windows/hardware/aa364204) 
- [FwpmSessionDestroyEnumHandle0](https://msdn.microsoft.com/library/windows/hardware/aa364205) 
- [FwpmSessionEnum0](https://msdn.microsoft.com/library/windows/hardware/aa364206) 

## <a name="sublayer-management"></a>副層の管理

- [FwpmSubLayerAdd0](https://msdn.microsoft.com/library/windows/hardware/aa364207) 
- [FwpmSubLayerCreateEnumHandle0](https://msdn.microsoft.com/library/windows/hardware/aa364208) 
- [FwpmSubLayerDeleteByKey0](https://msdn.microsoft.com/library/windows/hardware/aa364209) 
- [FwpmSubLayerDestroyEnumHandle0](https://msdn.microsoft.com/library/windows/hardware/aa364210) 
- [FwpmSubLayerEnum0](https://msdn.microsoft.com/library/windows/hardware/aa364211) 
- [FwpmSubLayerGetByKey0](https://msdn.microsoft.com/library/windows/hardware/aa364212) 
- [FwpmSubLayerGetSecurityInfoByKey0](https://msdn.microsoft.com/library/windows/hardware/aa364213) 
- [FwpmSubLayerSetSecurityInfoByKey0](https://msdn.microsoft.com/library/windows/hardware/aa364235) 

## <a name="transaction-management"></a>トランザクションの管理

- [FwpmTransactionAbort0](https://msdn.microsoft.com/library/windows/hardware/aa364242) 
- [FwpmTransactionBegin0](https://msdn.microsoft.com/library/windows/hardware/aa364243) 
- [FwpmTransactionCommit0](https://msdn.microsoft.com/library/windows/hardware/aa364245) 

## <a name="vswitch-management"></a>vSwitch の管理

- [FwpmvSwitchEventsGetSecurityInfo0](https://msdn.microsoft.com/library/windows/hardware/hh447339) 
- [FwpmvSwitchEventsSetSecurityInfo0](https://msdn.microsoft.com/library/windows/hardware/hh447341) 

