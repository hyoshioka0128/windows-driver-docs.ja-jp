---
title: メタデータ フィールド L2 識別子
description: このセクションでは、Windows Filtering Platform コールアウト ドライバーのメタデータ フィールド L2 識別子について説明します。
ms.assetid: 4A03C593-3760-48F0-A082-A9D1AD90EAD6
keywords:
- ネットワーク ドライバーをメタデータ フィールドの L2 識別子
ms.date: 11/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6fe05ff69fde74e2abf02e7efa41193ffe2fbbfd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581026"
---
# <a name="metadata-field-l2-identifiers"></a>メタデータ フィールド L2 識別子

Windows 8 および Windows Server 2012 は、メタデータ フィールドの L2 識別子を紹介します。

メタデータ フィールドの L2 識別子は、各ビット フィールドで表されます。 これらの識別子の定義は次のとおりです。

| メタデータ フィールドの識別子 | 説明 |
| --- | --- |
| FWPS_L2_METADATA_FIELD_ETHERNET_MAC_HEADER_SIZE | MAC ヘッダーのバイト単位のサイズ。 |
| FWPS_L2_METADATA_FIELD_VSWITCH_DESTINATION_PORT_ID | 仮想スイッチ上の宛先ポートの識別子。 |
| FWPS_L2_METADATA_FIELD_VSWITCH_PACKET_CONTEXT | A**処理**仮想スイッチ パケットのコンテキストにします。 |
| FWPS_L2_METADATA_FIELD_VSWITCH_SOURCE_NIC_INDEX | NIC、仮想スイッチ上のソースのインデックス。 |
| FWPS_L2_METADATA_FIELD_VSWITCH_SOURCE_PORT_ID | 仮想スイッチで発信元ポートの識別子。 |
| FWPS_L2_METADATA_FIELD_WIFI_OPERATION_MODE | 現在のネイティブの 802.11 操作モード。 |

## <a name="related-topics"></a>関連トピック

[メタデータ フィールドの識別子](metadata-field-identifiers.md)

[各フィルター レイヤーでのメタデータ フィールド](metadata-fields-at-each-filtering-layer.md)

[FWPS_INCOMING_METADATA_VALUES0](https://msdn.microsoft.com/library/windows/hardware/ff552397)

