---
title: 接続指向ミニポート ドライバーの一般操作 OID
description: このトピックでは、接続指向のオブジェクトの oid です。 一般的な運用について説明します。
ms.assetid: 38a8a256-b70e-4ba9-bc95-f1a2965493b2
keywords:
- '[全般] の運用 Oid 接続指向のミニポート ドライバー'
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3756d5b2ebd74d787342e585e516916dfd5e3680
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349922"
---
# <a name="general-operational-oids-for-connection-oriented-miniport-drivers"></a>接続指向ミニポート ドライバーの一般操作 OID

次の表は、接続指向のミニポート ドライバーの一般的な操作特性や、Nic 設定を取得または使用 Oid をまとめたものです。

> [!TIP] 
> 接続指向のミニポート ドライバーでは、このような要求を処理するその[MiniportCoOidRequest](https://msdn.microsoft.com/library/windows/hardware/ff559362)コールバック関数。

次の表では、M は、OID は必須では、O は、これは省略可能なことを示しますを示します。

| 長さ | クエリ | Set | 名前 |
| --- | --- | --- | --- |
| 2 | M |   | [OID_GEN_CO_DRIVER_VERSION](oid-gen-co-driver-version.md) |
| 8 | O |   | [OID_GEN_CO_GET_NETCARD_TIME](oid-gen-co-get-netcard-time.md) |
| 8 | O |   | [OID_GEN_CO_GET_TIME_CAPS](oid-gen-co-get-time-caps.md) |
| 4 | M |   | [OID_GEN_CO_HARDWARE_STATUS](oid-gen-co-hardware-status.md) |
| 4 | M |   | [OID_GEN_CO_LINK_SPEED](oid-gen-co-link-speed.md) |
| 4 | M |   | [OID_GEN_CO_MAC_OPTIONS](oid-gen-co-mac-options.md) |
| 4 | M |   | [OID_GEN_CO_MEDIA_CONNECT_STATUS](oid-gen-co-media-connect-status.md) |
| Arr(4) | M |   | [OID_GEN_CO_MEDIA_IN_USE](oid-gen-co-media-in-use.md) |
| Arr(4) | M |   | [OID_GEN_CO_MEDIA_SUPPORTED](oid-gen-co-media-supported.md) |
| 4 | M |   | [OID_GEN_CO_MINIMUM_LINK_SPEED](oid-gen-co-minimum-link-speed.md) |
| 4 |   | M | [OID_GEN_CO_PROTOCOL_OPTIONS](oid-gen-co-protocol-options.md) |
| arr | O |   | [OID_GEN_CO_SUPPORTED_GUIDS](oid-gen-co-supported-guids.md) |
| Arr(4) | M |   | [OID_GEN_CO_SUPPORTED_LIST](oid-gen-co-supported-list.md) |
| Var 関数 | M |   | [OID_GEN_CO_VENDOR_DESCRIPTION](oid-gen-co-vendor-description.md) |
| 4 | M |   | [OID_GEN_CO_VENDOR_DRIVER_VERSION](oid-gen-co-vendor-driver-version.md) |
| 4 | M |   | [OID_GEN_CO_VENDOR_ID](oid-gen-co-vendor-id.md) |

