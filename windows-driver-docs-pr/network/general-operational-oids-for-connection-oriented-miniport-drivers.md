---
title: 接続指向ミニポート ドライバーの一般操作 OID
description: このトピックでは、接続指向オブジェクトの一般的な操作 Oid について説明します。
ms.assetid: 38a8a256-b70e-4ba9-bc95-f1a2965493b2
keywords:
- 一般的な操作 Oid 接続指向ミニポートドライバー
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc85b857e7548c69183bbaf245f40acc519b849e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842188"
---
# <a name="general-operational-oids-for-connection-oriented-miniport-drivers"></a>接続指向ミニポート ドライバーの一般操作 OID

次の表は、接続指向のミニポートドライバーや Nic の一般的な動作特性を取得または設定するために使用される Oid をまとめたものです。

> [!TIP] 
> 接続指向のミニポートドライバーは、そのような要求を[MiniportCoOidRequest](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_oid_request)コールバック関数で処理します。

この表では、M は OID が必須であることを示していますが、O は省略可能であることを示しています。

| 長さ | クエリ | 設定 | 名前 |
| --- | --- | --- | --- |
| 2 | [M] |   | [OID_GEN_CO_DRIVER_VERSION](oid-gen-co-driver-version.md) |
| 8 | O |   | [OID_GEN_CO_GET_NETCARD_TIME](oid-gen-co-get-netcard-time.md) |
| 8 | O |   | [OID_GEN_CO_GET_TIME_CAPS](oid-gen-co-get-time-caps.md) |
| ホーム フォルダーが置かれているコンピューターにアクセスできない | [M] |   | [OID_GEN_CO_HARDWARE_STATUS](oid-gen-co-hardware-status.md) |
| ホーム フォルダーが置かれているコンピューターにアクセスできない | [M] |   | [OID_GEN_CO_LINK_SPEED](oid-gen-co-link-speed.md) |
| ホーム フォルダーが置かれているコンピューターにアクセスできない | [M] |   | [OID_GEN_CO_MAC_OPTIONS](oid-gen-co-mac-options.md) |
| ホーム フォルダーが置かれているコンピューターにアクセスできない | [M] |   | [OID_GEN_CO_MEDIA_CONNECT_STATUS](oid-gen-co-media-connect-status.md) |
| Arr (4) | [M] |   | [OID_GEN_CO_MEDIA_IN_USE](oid-gen-co-media-in-use.md) |
| Arr (4) | [M] |   | [OID_GEN_CO_MEDIA_SUPPORTED](oid-gen-co-media-supported.md) |
| ホーム フォルダーが置かれているコンピューターにアクセスできない | [M] |   | [OID_GEN_CO_MINIMUM_LINK_SPEED](oid-gen-co-minimum-link-speed.md) |
| ホーム フォルダーが置かれているコンピューターにアクセスできない |   | [M] | [OID_GEN_CO_PROTOCOL_OPTIONS](oid-gen-co-protocol-options.md) |
| → | O |   | [OID_GEN_CO_SUPPORTED_GUIDS](oid-gen-co-supported-guids.md) |
| Arr (4) | [M] |   | [OID_GEN_CO_SUPPORTED_LIST](oid-gen-co-supported-list.md) |
| Var. | [M] |   | [OID_GEN_CO_VENDOR_DESCRIPTION](oid-gen-co-vendor-description.md) |
| ホーム フォルダーが置かれているコンピューターにアクセスできない | [M] |   | [OID_GEN_CO_VENDOR_DRIVER_VERSION](oid-gen-co-vendor-driver-version.md) |
| ホーム フォルダーが置かれているコンピューターにアクセスできない | [M] |   | [OID_GEN_CO_VENDOR_ID](oid-gen-co-vendor-id.md) |

