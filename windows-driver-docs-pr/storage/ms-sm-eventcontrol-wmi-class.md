---
title: MS\_SM\_EventControl WMI クラス
description: MS\_SM\_EventControl WMI クラス
ms.assetid: d5c6a308-2782-4846-81f9-f4932d8caac6
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7fcaabce0bc75481e007dc1421f050356e72f7c6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577677"
---
# <a name="mssmeventcontrol-wmi-class"></a>MS\_SM\_EventControl WMI クラス


MS\_SM\_EventControl WMI クラスが WMI クライアントがリンク、ポート、およびターゲット イベントの配信を制御できるようにする WMI メソッドを定義します。 この WMI クラスには、データ ブロックがありません。 そのため、WMI ツールのスイートには、クラスに属するメソッドのパラメーター データを格納する構造体の宣言が生成されますが、クラス自体に対応する構造体の宣言を生成しません。

このクラスに属している各メソッドの MOF 構文は、メソッドのリファレンス ページの説明です。 次のトピックでは、これらのメソッドとそれらに付随する構造体について説明します。

[**SM\_AddTarget**](sm-addtarget.md)

[**SM\_RemoveTarget**](sm-removetarget.md)

[**SM\_AddPort**](sm-addport.md)

[**SM\_RemovePort**](sm-removeport.md)

[**SM\_AddLink**](sm-addlink.md)

[**SM\_RemoveLink**](sm-removelink.md)

MS\_SM\_EventControl クラスが次のように定義されている*Hbaapi.mof*:

```cpp
class MS_SM_EventControl 
{ 
    [key] 
    string  InstanceName; 
    boolean Active; 

    //
    // These methods are used to control delivery of MS_SM_TargetEvents
//
    [ Implemented, WmiMethodId(1) ]
    void SM_AddTarget(
            [in, HBAType("HBA_WWN") ] uint8 HbaPortWWN[8],
            [in, HBAType("HBA_WWN") ] uint8 DiscoveredPortWWN[8],
            [in, HBAType("HBA_WWN") ] uint8 DomainPortWWN[8],
            [in ] uint32  AllTargets,
            [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus
            );

    [ Implemented, WmiMethodId(2) ]
    void SM_RemoveTarget(
            [in, HBAType("HBA_WWN") ] uint8 HbaPortWWN[8],
            [in, HBAType("HBA_WWN") ] uint8 DiscoveredPortWWN[8],
            [in, HBAType("HBA_WWN") ] uint8 DomainPortWWN[8],
            [in ] uint32  AllTargets,
            [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus
            );


//
// These methods are used to control delivery of MS_SM_PortEvents
//
    [ Implemented, WmiMethodId(3) ]
    void SM_AddPort(
            [in, HBAType("HBA_WWN") ] uint8 PortWWN[8],
            [in, EVENT_TYPES_QUALIFIERS ] uint32 EventType,
            [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus
            );

    [ Implemented, WmiMethodId(4) ]
    void SM_RemovePort(
            [in, HBAType("HBA_WWN") ] uint8 PortWWN[8],
            [in, EVENT_TYPES_QUALIFIERS ] uint32 EventType,
            [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus
            );

//
// These methods are used to control delivery of MSFC_LinkEvents
//
    [ Implemented, WmiMethodId(10) ]
    void SM_AddLink(
            [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus
            );

    [ Implemented, WmiMethodId(11) ]
    void SM_RemoveLink(
            [out, HBA_STATUS_QUALIFIERS ] HBA_STATUS HBAStatus
            );
};
```

 

 





