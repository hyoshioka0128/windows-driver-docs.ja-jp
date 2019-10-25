---
title: メタデータ フィールド L2 識別子
description: このセクションでは、Windows フィルタリングプラットフォームのコールアウトドライバーのメタデータフィールド L2 識別子について説明します。
ms.assetid: 4A03C593-3760-48F0-A082-A9D1AD90EAD6
keywords:
- メタデータフィールド L2 識別子ネットワークドライバー
ms.date: 11/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8f11b8cff5b8d980dd8b8af08520b3fd4cfcbb9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844263"
---
# <a name="metadata-field-l2-identifiers"></a>メタデータ フィールド L2 識別子

Windows 8 と Windows Server 2012 では、メタデータフィールド L2 識別子が導入されています。

メタデータフィールド L2 識別子は、それぞれビットフィールドによって表されます。 これらの識別子は次のように定義されます。

| メタデータフィールド識別子 | 説明 |
| --- | --- |
| FWPS_L2_METADATA_FIELD_ETHERNET_MAC_HEADER_SIZE | MAC ヘッダーのサイズ (バイト単位)。 |
| FWPS_L2_METADATA_FIELD_VSWITCH_DESTINATION_PORT_ID | 仮想スイッチの宛先ポートの識別子。 |
| FWPS_L2_METADATA_FIELD_VSWITCH_PACKET_CONTEXT | 仮想スイッチパケットコンテキストを**処理するハンドル**。 |
| FWPS_L2_METADATA_FIELD_VSWITCH_SOURCE_NIC_INDEX | 仮想スイッチのソース NIC のインデックス。 |
| FWPS_L2_METADATA_FIELD_VSWITCH_SOURCE_PORT_ID | 仮想スイッチの送信元ポートの識別子。 |
| FWPS_L2_METADATA_FIELD_WIFI_OPERATION_MODE | 現在のネイティブ802.11 操作モード。 |

## <a name="related-topics"></a>関連トピック

[メタデータフィールド識別子](metadata-field-identifiers.md)

[各フィルターレイヤーのメタデータフィールド](metadata-fields-at-each-filtering-layer.md)

[FWPS_INCOMING_METADATA_VALUES0](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_incoming_metadata_values0_)

