---
title: GUID_NDIS_GEN_STATISTICS
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_GEN_STATISTICS について説明します。
ms.assetid: 3751d4e7-7991-4329-9eb2-6a44ca1190d4
keywords:
- GUID_NDIS_GEN_STATISTICS、WDK GUID_NDIS_GEN_STATISTICS ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e762230f007223f8fc40efb30307c30739a5a30
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382697"
---
# <a name="guidndisgenstatistics"></a>GUID_NDIS_GEN_STATISTICS

WMI クライアントは、GUID GUID_NDIS_GEN_STATISTICS メソッドを使用して、ミニポート アダプタの統計情報を取得できます。 この WMI GUID は、NDIS 6.0 および以降のバージョンでサポートされます。

WMI クライアント GUID_NDIS_GEN_STATISTICS WMI メソッドの要求を発行と NDIS ミニポート アダプターまたは NDIS ポートの現在の統計情報を返します。 WMI のメソッド識別子は NDIS_WMI_DEFAULT_METHOD_ID、する必要があり、WMI の入力バッファーに格納する必要があります、 [NDIS_WMI_METHOD_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_wmi_method_header)構造体。

NDIS を使用して、 [OID_GEN_STATISTICS](oid-gen-statistics.md)ミニポート アダプターの統計情報を取得する OID。 この OID は、NDIS 6.0 とそれ以降のバージョンをサポートするミニポート ドライバーに対して必須です。 統計カウンターは、符号なし 64 ビット値です。 ミニポート ドライバーでは、NDIS_STATISTICS_INFO 構造体内の統計を返します。

GUID を持つ NDIS が返すデータ バッファーには、NDIS_STATISTICS_INFO 構造体が含まれています。

