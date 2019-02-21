---
title: NetAdapterCx クライアント ドライバーの INF ファイル
description: NetAdapterCx クライアント ドライバーの INF ファイル
ms.assetid: B885CDF7-B399-440B-A385-27F1090B9C56
keywords:
- NetAdapterCx クライアント ドライバー、NetCx INF ファイル、NetAdapterCx INF の INF ファイル
ms.date: 08/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 5265147b4d1bd47c16f0e46ba5dc4508d805fd4f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553825"
---
# <a name="inf-files-for-netadaptercx-client-drivers"></a>NetAdapterCx クライアント ドライバーの INF ファイル

[!include[NetAdapterCx Beta Prerelease](../netcx-beta-prerelease.md)]

NetAdapterCx クライアント ドライバーの INF ファイルは、標準的なネットワーク INF ファイルでは、いくつかその他のキーワード NetAdapterCx に固有の上に構築します。 

標準的なネットワーク INF ファイルの詳細については、次を参照してください。[ネットワーク INF ファイルの作成](../network/creating-network-inf-files.md)です。 基本の INF ファイルの詳細については、次を参照してください。 [INF ファイルのセクションとディレクティブ](../install/inf-file-sections-and-directives.md)します。

次の表では、新しい NetAdapterCx INF キーワードについて説明します。

| 新しいネットワーク キーワード | INF ファイルのセクション | 省略可能または必須 | 説明 |
| --- | --- | --- | --- |
| **\*IfConnectorPresent** | Device.NT | 必須 | <p>コネクタが存在するかどうかを示すブール値。 このキーワードを設定**1**、または**TRUE**物理アダプターがある場合、します。</p> <p>**注**置換、 **IfConnectorPresent**フィールドを[ **NDIS_MINIPORT_ADAPTER_GENERAL_ATTRIBUTES** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)構造体。</p> |
| **\*ConnectionType** | Device.NT | 必須 | A [ **NET_IF_CONNECTION_TYPE** ](https://docs.microsoft.com/windows/desktop/api/ifdef/ne-ifdef-_net_if_connection_type)を指定する値、[ネットワーク インターフェイスの NDIS](../network/ndis-network-interfaces2.md)接続の種類。 |
| **\*DirectionType** | Device.NT | 必須 | A [ **NET_IF_DIRECTION_TYPE** ](https://docs.microsoft.com/windows/desktop/api/ifdef/ne-ifdef-_net_if_direction_type)を指定する値、[ネットワーク インターフェイスの NDIS](../network/ndis-network-interfaces2.md)方向の種類。 |
| **\*AccessType** | Device.NT | 必須 | A [ **NET_IF_ACCESS_TYPE** ](https://docs.microsoft.com/windows/desktop/api/ifdef/ne-ifdef-_net_if_access_type)を指定する値、[ネットワーク インターフェイスの NDIS](../network/ndis-network-interfaces2.md)アクセスの種類。 |
| **\*HardwareLoopback** | Device.NT | 必須 | <p>ネットワーク インターフェイス カード (NIC) にハードウェア ループバックのサポートが含まれるかどうかを示すブール値。</p> <p>**注**このキーワードに設定**1**、または**TRUE**のと同じ**いない**設定、 **NDIS_MAC_OPTION_NO_LOOPBACK**フラグ、 **MacOptions**のフィールド、 [ **NDIS_MINIPORT_ADAPTER_GENERAL_ATTRIBUTES** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)構造体。</p> |
| **NumberOfNetworkInterfaces** | Device.NT | 省略可能 | 数のネットワーク インターフェイス、NIC がサポートを指定します。 NIC にデバイスごとに 1 つ以上のネットワーク インターフェイスがサポートするかどうかにのみ必要です。 |

次に、例を示します。

```INF
[Device.NT]
CopyFiles=Drivers_Dir

; Existing network keywords
*IfType       = 6
*MediaType     = 0
*PhysicalMediaType = 14

; New network keywords
*IfConnectorPresent = 1     ; BOOLEAN
*ConnectionType   = 1       ; NET_IF_CONNECTION_TYPE
*DirectionType   = 0        ; NET_IF_DIRECTION_TYPE
*AccessType     = 2         ; NET_IF_ACCESS_TYPE
*HardwareLoopback  = 0      ; BOOLEAN
NumberOfNetworkInterfaces = 11
```
