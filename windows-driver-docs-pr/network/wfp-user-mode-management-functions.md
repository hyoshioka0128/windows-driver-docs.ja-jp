---
title: WFP ユーザー モード管理関数
description: このトピックでは、WFP ユーザー モードの管理機能について説明します。
ms.assetid: 14accd49-5b96-40]()e6-b9d7-6638a4e5c2dc
keywords:
- WFP ユーザー モードの管理機能はネットワーク ドライバー
ms.date: 11/07/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89e191460ca41a1bac4b29716be72d0f6f4bc60a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370562"
---
# <a name="wfp-user-mode-management-functions"></a>WFP ユーザー モード管理関数

Windows フィルタ リング プラットフォームのユーザー モードの管理機能のセマンティクスはまったく同じから呼び出されるとコールアウト ドライバーとして、ユーザー モード アプリケーションから呼び出されたときに、戻り値の型がある点が、 **NTSTATUS**コードWin32 エラー コードではなく。 

これらの関数が記載されて、[管理機能](https://docs.microsoft.com/windows/desktop/FWP/fwp-mgmt-functions)ユーザー モードの[WFP 関数](https://docs.microsoft.com/windows/desktop/FWP/fwp-functions)ドキュメント。 

> [!NOTE]
> 各関数のカーネル モード バージョンは、fwpmk.h で定義されます。 各関数のユーザー モード バージョンは、fwpmu.h で定義されます。
 
これらの関数を除くのすべての呼び出し元[FwpmFreeMemory0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfreememory0) IRQL で実行する必要があります PASSIVE_LEVEL を = です。 呼び出し元**FwpmFreeMemory0** IRQL で実行する必要があります < = DISPATCH_LEVEL します。

## <a name="callout-management"></a>引き出し線の管理

- [FwpmCalloutAdd0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmcalloutadd0) 
- [FwpmCalloutCreateEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmcalloutcreateenumhandle0) 
- [FwpmCalloutDeleteById0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmcalloutdeletebyid0) 
- [FwpmCalloutDeleteByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmcalloutdeletebykey0) 
- [FwpmCalloutDestroyEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmcalloutdestroyenumhandle0) 
- [FwpmCalloutEnum0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmcalloutenum0) 
- [FwpmCalloutGetById0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmcalloutgetbyid0) 
- [FwpmCalloutGetByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmcalloutgetbykey0) 
- [FwpmCalloutGetSecurityInfoByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmcalloutgetsecurityinfobykey0) 
- [FwpmCalloutSetSecurityInfoByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmcalloutsetsecurityinfobykey0) 

## <a name="connection-object-management"></a>接続オブジェクトの管理

- [FwpmConnectionCreateEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmconnectioncreateenumhandle0) 
- [FwpmConnectionDestroyEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmconnectiondestroyenumhandle0) 
- [FwpmConnectionEnum0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmconnectionenum0) 
- [FwpmConnectionGetById0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmconnectiongetbyid0) 
- [FwpmConnectionGetSecurityInfo0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmconnectiongetsecurityinfo0) 
- [FwpmConnectionSetSecurityInfo0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmconnectionsetsecurityinfo0) 

## <a name="event-management"></a>イベントの管理

- [FwpmNetEventCreateEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmneteventcreateenumhandle0) 
- [FwpmNetEventDestroyEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmneteventdestroyenumhandle0) 
- FwpmNetEventEnum:
    - [FwpmNetEventEnum0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmneteventenum0) (Windows Vista)
    - [FwpmNetEventEnum1](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmneteventenum1) (Windows 7)
    - [FwpmNetEventEnum2](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmneteventenum2) (Windows 8)
- [FwpmNetEventsGetSecurityInfo0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmneteventsgetsecurityinfo0) 
- [FwpmNetEventsSetSecurityInfo0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmneteventssetsecurityinfo0) 

## <a name="filter-management"></a>フィルターの管理

- [FwpmFilterAdd0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfilteradd0) 
- [FwpmFilterCreateEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfiltercreateenumhandle0) 
- [FwpmFilterDeleteById0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfilterdeletebyid0) 
- [FwpmFilterDeleteByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfilterdeletebykey0) 
- [FwpmFilterDestroyEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfilterdestroyenumhandle0) 
- [FwpmFilterEnum0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfilterenum0) 
- [FwpmFilterGetById0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfiltergetbyid0) 
- [FwpmFilterGetByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfiltergetbykey0) 
- [FwpmFilterGetSecurityInfoByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfiltergetsecurityinfobykey0) 
- [FwpmFilterSetSecurityInfoByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmfiltersetsecurityinfobykey0) 

## <a name="layer-management"></a>レイヤーの管理

- [FwpmLayerCreateEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmlayercreateenumhandle0) 
- [FwpmLayerDestroyEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmlayerdestroyenumhandle0) 
- [FwpmLayerEnum0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmlayerenum0) 
- [FwpmLayerGetById0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmlayergetbyid0) 
- [FwpmLayerGetByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmlayergetbykey0) 
- [FwpmLayerGetSecurityInfoByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmlayergetsecurityinfobykey0) 
- [FwpmLayerSetSecurityInfoByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmlayersetsecurityinfobykey0) 

## <a name="provider-context-management"></a>プロバイダー コンテキストの管理

- [FwpmProviderContextAdd:
    - [FwpmProviderContextAdd0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextadd0) (Windows Vista)
    - [FwpmProviderContextAdd1](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextadd1) (Windows 7)
    - [FwpmProviderContextAdd2](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextadd2) (Windows 8)
- [FwpmProviderContextCreateEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextcreateenumhandle0) 
- [FwpmProviderContextDeleteById0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextdeletebyid0) 
- [FwpmProviderContextDeleteByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextdeletebykey0) 
- [FwpmProviderContextDestroyEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextdestroyenumhandle0) 
- FwpmProviderContextEnum:
    - [FwpmProviderContextEnum0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextenum0) (Windows Vista)
    - [FwpmProviderContextEnum1](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextenum1) (Windows 7)
    - [FwpmProviderContextEnum2](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextenum2) (Windows 8)
- FwpmProviderContextGetById:
    - [FwpmProviderContextGetById0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextgetbyid0) (Windows Vista)
    - [FwpmProviderContextGetById1](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextgetbyid1) (Windows 7)
    - [FwpmProviderContextGetById2](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextgetbyid2) (Windows 8)
- FwpmProviderContextGetByKey:
    - [FwpmProviderContextGetByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextgetbykey0) (Windows Vista)
    - [FwpmProviderContextGetByKey1](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextgetbykey1) (Windows 7)
    - [FwpmProviderContextGetByKey2](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextgetbykey2) (Windows 8)
- [FwpmProviderContextGetSecurityInfoByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextgetsecurityinfobykey0) 
- [FwpmProviderContextSetSecurityInfoByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercontextsetsecurityinfobykey0) 

## <a name="provider-management"></a>プロバイダーの管理

- [FwpmProviderAdd0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovideradd0) 
- [FwpmProviderCreateEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidercreateenumhandle0) 
- [FwpmProviderDeleteByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmproviderdeletebykey0) 
- [FwpmProviderDestroyEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmproviderdestroyenumhandle0) 
- [FwpmProviderEnum0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmproviderenum0) 
- [FwpmProviderGetByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidergetbykey0) 
- [FwpmProviderGetSecurityInfoByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidergetsecurityinfobykey0) 
- [FwpmProviderSetSecurityInfoByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmprovidersetsecurityinfobykey0) 

## <a name="session-management"></a>セッションの管理

- [FwpmEngineClose0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmengineclose0) 
- [FwpmEngineGetOption0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmenginegetoption0) 
- [FwpmEngineGetSecurityInfo0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmenginegetsecurityinfo0) 
- [FwpmEngineOpen0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmengineopen0) 
- [FwpmEngineSetOption0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmenginesetoption0) 
- [FwpmEngineSetSecurityInfo0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmenginesetsecurityinfo0) 
- [FwpmSessionCreateEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsessioncreateenumhandle0) 
- [FwpmSessionDestroyEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsessiondestroyenumhandle0) 
- [FwpmSessionEnum0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsessionenum0) 

## <a name="sublayer-management"></a>副層の管理

- [FwpmSubLayerAdd0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsublayeradd0) 
- [FwpmSubLayerCreateEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsublayercreateenumhandle0) 
- [FwpmSubLayerDeleteByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsublayerdeletebykey0) 
- [FwpmSubLayerDestroyEnumHandle0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsublayerdestroyenumhandle0) 
- [FwpmSubLayerEnum0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsublayerenum0) 
- [FwpmSubLayerGetByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsublayergetbykey0) 
- [FwpmSubLayerGetSecurityInfoByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsublayergetsecurityinfobykey0) 
- [FwpmSubLayerSetSecurityInfoByKey0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmsublayersetsecurityinfobykey0) 

## <a name="transaction-management"></a>トランザクションの管理

- [FwpmTransactionAbort0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmtransactionabort0) 
- [FwpmTransactionBegin0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmtransactionbegin0) 
- [FwpmTransactionCommit0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmtransactioncommit0) 

## <a name="vswitch-management"></a>vSwitch の管理

- [FwpmvSwitchEventsGetSecurityInfo0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmvswitcheventsgetsecurityinfo0) 
- [FwpmvSwitchEventsSetSecurityInfo0](https://docs.microsoft.com/windows/desktop/api/fwpmu/nf-fwpmu-fwpmvswitcheventssetsecurityinfo0) 

