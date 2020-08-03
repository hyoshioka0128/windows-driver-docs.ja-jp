---
title: NetAdapterCx クライアント ドライバーの INF ファイル
description: NetAdapterCx クライアント ドライバーの INF ファイル
ms.assetid: B885CDF7-B399-440B-A385-27F1090B9C56
keywords:
- NetAdapterCx クライアントドライバー、NetCx INF ファイル、NetAdapterCx INF 用の INF ファイル
ms.date: 08/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3f8638c46f73a09eed74f3bc0d02bdc72952a20d
ms.sourcegitcommit: 20a89aa2cb2c6385c2a49ebf78e5797c821d87ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/31/2020
ms.locfileid: "87473734"
---
# <a name="inf-files-for-netadaptercx-client-drivers"></a>NetAdapterCx クライアント ドライバーの INF ファイル

NetAdapterCx クライアントドライバー用の INF ファイルは、標準のネットワーク INF ファイルの上に構築されており、NetAdapterCx に固有のキーワードがいくつかあります。 

標準的なネットワーク INF ファイルの詳細については、「[ネットワーク Inf ファイルの作成](../network/creating-network-inf-files.md)」を参照してください。 基本の INF ファイルの詳細については、「 [inf ファイルの概要](../install/overview-of-inf-files.md)」を参照してください。

次の表では、NetAdapterCx の新しい INF キーワードについて説明します。

| 新しいネットワークキーワード | INF ファイルセクション | 省略可能または必須 | Description |
| --- | --- | --- | --- |
| **\*Ifコネクターが存在します** | Device. NT | 必須 | <p>コネクタが存在するかどうかを示すブール値です。 物理アダプターがある場合は、このキーワードを**1**または**TRUE**に設定します。</p> <p>**メモ**[**NDIS_MINIPORT_ADAPTER_GENERAL_ATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)構造体の**Ifコネクターの存在**フィールドを置き換えます。</p> |
| **\*ConnectionType** | Device. NT | 必須 | [NDIS ネットワークインターフェイス](../network/ndis-network-interfaces2.md)の接続の種類を示す[**NET_IF_CONNECTION_TYPE**](https://docs.microsoft.com/windows/desktop/api/ifdef/ne-ifdef-_net_if_connection_type)値です。 |
| **\*Direction 型** | Device. NT | 必須 | [NDIS ネットワークインターフェイス](../network/ndis-network-interfaces2.md)の方向の種類を示す[**NET_IF_DIRECTION_TYPE**](https://docs.microsoft.com/windows/desktop/api/ifdef/ne-ifdef-_net_if_direction_type)値です。 |
| **\*AccessType** | Device. NT | 必須 | [NDIS ネットワークインターフェイス](../network/ndis-network-interfaces2.md)のアクセスの種類を指定する[**NET_IF_ACCESS_TYPE**](https://docs.microsoft.com/windows/desktop/api/ifdef/ne-ifdef-_net_if_access_type)値。 |
| **\*ハードウェアループバック** | Device. NT | 必須 | <p>ネットワークインターフェイスカード (NIC) にハードウェアループバックがサポートされているかどうかを示すブール値。</p> <p>**メモ**このキーワードを**1**または**TRUE**に設定することは、 [**NDIS_MINIPORT_ADAPTER_GENERAL_ATTRIBUTES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_general_attributes)構造体の**macoptions**フィールドに**NDIS_MAC_OPTION_NO_LOOPBACK**フラグを設定し**ないこと**と同じです。</p> |
| **NumberOfNetworkInterfaces** | Device. NT | 省略可能 | NIC がサポートするネットワークインターフェイスの数を指定します。 NIC がデバイスごとに複数のネットワークインターフェイスをサポートしている場合にのみ必要です。 |

次に例を示します。

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
