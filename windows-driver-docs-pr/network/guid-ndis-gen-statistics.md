---
title: GUID_NDIS_GEN_STATISTICS
description: このトピックでは、NDIS WMI インターフェイスの GUID_NDIS_GEN_STATISTICS GUID について説明します。
ms.assetid: 3751d4e7-7991-4329-9eb2-6a44ca1190d4
keywords:
- GUID_NDIS_GEN_STATISTICS、WDK GUID_NDIS_GEN_STATISTICS ネットワークドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fa57d8fc5b6ffa4d1817864534fbef7793222ea
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842282"
---
# <a name="guid_ndis_gen_statistics"></a>GUID_NDIS_GEN_STATISTICS

WMI クライアントは、GUID_NDIS_GEN_STATISTICS メソッド GUID を使用して、ミニポートアダプターの統計情報を取得できます。 この WMI GUID は、NDIS 6.0 以降のバージョンでサポートされています。

WMI クライアントが GUID_NDIS_GEN_STATISTICS WMI メソッド要求を発行すると、NDIS はミニポートアダプターまたは NDIS ポートの現在の統計情報を返します。 WMI メソッド識別子は NDIS_WMI_DEFAULT_METHOD_ID であり、WMI 入力バッファーには[NDIS_WMI_METHOD_HEADER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_method_header)構造体が含まれている必要があります。

NDIS は、 [OID_GEN_STATISTICS](oid-gen-statistics.md) OID を使用して、ミニポートアダプターの統計情報を取得します。 この OID は、NDIS 6.0 以降のバージョンをサポートするミニポートドライバーに必須です。 統計カウンターは、符号なし64ビット値です。 ミニポートドライバーは、NDIS_STATISTICS_INFO 構造の統計情報を返します。

NDIS によって GUID と共に返されるデータバッファーには、NDIS_STATISTICS_INFO 構造体が含まれています。

