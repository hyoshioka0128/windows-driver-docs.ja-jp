---
title: Hyper-V 拡張可能スイッチ OID
description: このセクションでは、HYPER-V 拡張可能スイッチの Oid とその特性について説明します。
keywords:
- Hyper-V 拡張可能スイッチ OID
- HYPER-V スイッチの Oid
- WDK の HYPER-V 拡張可能スイッチの Oid
- HYPER-V 拡張可能スイッチのオブジェクト識別子
ms.assetid: A97C5BF0-7319-4BEE-ABF7-12B11CEAF3DB"
ms.date: 04/24/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7034925cfc6b7187bf9cacf8e49738c9952d7a67
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581446"
---
# <a name="hyper-v-extensible-switch-oids"></a>Hyper-V 拡張可能スイッチ OID

このセクションでは、HYPER-V 拡張可能スイッチのオブジェクト識別子 (Oid) について説明します。 これらの Oid は、拡張可能スイッチ拡張機能または HYPER-V 拡張可能スイッチの拡張機能のいずれかによって発行できます。

次の表では、拡張可能スイッチの Oid の特性を定義します。 次の省略形を使用して、テーブルの Oid の特性を指定します。

- Q  
OID は、クエリ要求でのみ使用されます。
- S  
OID は、一連の要求でのみ使用されます。
- M  
OID は、メソッドの要求でのみ使用されます。 セットまたはクエリ操作のこれらの要求を発行する可能性があります。
- P  
拡張可能スイッチのプロトコルの端では、OID 要求が発行されます。 拡張機能には、拡張可能スイッチ、そのポートまたはポートに接続されている仮想ネットワーク アダプターに関する情報を取得する OID 要求の結果を確認できます。
- E  
拡張機能により、OID 要求が発行されます。

| 名前                                                                                                 | Q | S | M | P | E |
|---                                                                                                   |---|---|---|---|---|
| [OID_SWITCH_FEATURE_STATUS_QUERY](https://msdn.microsoft.com/library/windows/hardware/hh598260)      |   |   | x | x |   | 
| [OID_SWITCH_NIC_ARRAY](https://msdn.microsoft.com/library/windows/hardware/hh598261)                 | x |   |   |   | x | 
| [OID_SWITCH_NIC_CONNECT](https://msdn.microsoft.com/library/windows/hardware/hh598262)               |   | x |   | x |   |
| [OID_SWITCH_NIC_CREATE](https://msdn.microsoft.com/library/windows/hardware/hh598263)                |   | x |   | x |   |
| [OID_SWITCH_NIC_DELETE](https://msdn.microsoft.com/library/windows/hardware/hh598264)                |   | x |   | x |   |  
| [OID_SWITCH_NIC_DISCONNECT](https://msdn.microsoft.com/library/windows/hardware/hh598265)            |   | x |   | x |   | 
| [OID_SWITCH_NIC_REQUEST](https://msdn.microsoft.com/library/windows/hardware/hh598266)               |   |   | x |   | x |   
| [OID_SWITCH_NIC_RESTORE](https://msdn.microsoft.com/library/windows/hardware/hh598267)               |   | x |   | x |   |   
| [OID_SWITCH_NIC_SAVE](https://msdn.microsoft.com/library/windows/hardware/hh598268)                  | x |   |   | x |   |
| [OID_SWITCH_NIC_SAVE_COMPLETE](https://msdn.microsoft.com/library/windows/hardware/hh598269)         |   | x |   | x |   | 
| [OID_SWITCH_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/hh598270)                | x |   |   |   | x |
| [OID_SWITCH_PORT_ARRAY](https://msdn.microsoft.com/library/windows/hardware/hh598271)                | x |   |   |   | x | 
| [OID_SWITCH_PORT_CREATE](https://msdn.microsoft.com/library/windows/hardware/hh598272)               |   | x |   | x |   | 
| [OID_SWITCH_PORT_DELETE](https://msdn.microsoft.com/library/windows/hardware/hh598273)               |   | x |   | x |   | 
| [OID_SWITCH_PORT_FEATURE_STATUS_QUERY](https://msdn.microsoft.com/library/windows/hardware/hh598274) |   |   | x | x |   | 
| [OID_SWITCH_PORT_PROPERTY_ADD](https://msdn.microsoft.com/library/windows/hardware/hh598275)         |   | x |   | x |   |
| [OID_SWITCH_PORT_PROPERTY_DELETE](https://msdn.microsoft.com/library/windows/hardware/hh598276)      |   | x |   | x |   |   
| [OID_SWITCH_PORT_PROPERTY_ENUM](https://msdn.microsoft.com/library/windows/hardware/hh598277)        |   |   | x |   | x |   
| [OID_SWITCH_PORT_PROPERTY_UPDATE](https://msdn.microsoft.com/library/windows/hardware/hh598278)      |   | x |   | x |   | 
| [OID_SWITCH_PORT_TEARDOWN](https://msdn.microsoft.com/library/windows/hardware/hh598279)             |   | x |   | x |   |
| [OID_SWITCH_PROPERTY_ADD](https://msdn.microsoft.com/library/windows/hardware/hh598280)              |   | x |   | x |   | 
| [OID_SWITCH_PROPERTY_DELETE](https://msdn.microsoft.com/library/windows/hardware/hh598281)           |   | x |   | x |   | 
| [OID_SWITCH_PROPERTY_ENUM](https://msdn.microsoft.com/library/windows/hardware/hh598282)             |   |   | x |   | x |
| [OID_SWITCH_PROPERTY_UPDATE](https://msdn.microsoft.com/library/windows/hardware/hh598283)           |   | x |   | x |   | 


