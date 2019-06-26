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
ms.openlocfilehash: 6883f1b216449c57c9f6926434a901902e21494f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382215"
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
| [OID_SWITCH_FEATURE_STATUS_QUERY](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-feature-status-query)      |   |   | x | x |   | 
| [OID_SWITCH_NIC_ARRAY](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-array)                 | x |   |   |   | x | 
| [OID_SWITCH_NIC_CONNECT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-connect)               |   | x |   | x |   |
| [OID_SWITCH_NIC_CREATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-create)                |   | x |   | x |   |
| [OID_SWITCH_NIC_DELETE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-delete)                |   | x |   | x |   |  
| [OID_SWITCH_NIC_DISCONNECT](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-disconnect)            |   | x |   | x |   | 
| [OID_SWITCH_NIC_REQUEST](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-request)               |   |   | x |   | x |   
| [OID_SWITCH_NIC_RESTORE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-restore)               |   | x |   | x |   |   
| [OID_SWITCH_NIC_SAVE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save)                  | x |   |   | x |   |
| [OID_SWITCH_NIC_SAVE_COMPLETE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-nic-save-complete)         |   | x |   | x |   | 
| [OID_SWITCH_PARAMETERS](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-parameters)                | x |   |   |   | x |
| [OID_SWITCH_PORT_ARRAY](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-array)                | x |   |   |   | x | 
| [OID_SWITCH_PORT_CREATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-create)               |   | x |   | x |   | 
| [OID_SWITCH_PORT_DELETE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-delete)               |   | x |   | x |   | 
| [OID_SWITCH_PORT_FEATURE_STATUS_QUERY](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-feature-status-query) |   |   | x | x |   | 
| [OID_SWITCH_PORT_PROPERTY_ADD](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-add)         |   | x |   | x |   |
| [OID_SWITCH_PORT_PROPERTY_DELETE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-delete)      |   | x |   | x |   |   
| [OID_SWITCH_PORT_PROPERTY_ENUM](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-enum)        |   |   | x |   | x |   
| [OID_SWITCH_PORT_PROPERTY_UPDATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-property-update)      |   | x |   | x |   | 
| [OID_SWITCH_PORT_TEARDOWN](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-port-teardown)             |   | x |   | x |   |
| [OID_SWITCH_PROPERTY_ADD](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-add)              |   | x |   | x |   | 
| [OID_SWITCH_PROPERTY_DELETE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-delete)           |   | x |   | x |   | 
| [OID_SWITCH_PROPERTY_ENUM](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-enum)             |   |   | x |   | x |
| [OID_SWITCH_PROPERTY_UPDATE](https://docs.microsoft.com/windows-hardware/drivers/network/oid-switch-property-update)           |   | x |   | x |   | 


