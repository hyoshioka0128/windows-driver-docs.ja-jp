---
title: GUID_NDIS_ENUMERATE_ADAPTERS_EX
description: このトピックでは、NDIS WMI インターフェイスの GUID_NDIS_ENUMERATE_ADAPTERS_EX GUID について説明します。
ms.assetid: 46c4c127-a9f6-4555-82d1-3c537fbb7914
keywords:
- GUID_NDIS_ENUMERATE_ADAPTERS_EX、WDK GUID_NDIS_ENUMERATE_ADAPTERS_EX ネットワークドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e9f9ca45bfda7fa968277f62a4c8d9961a613f8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842176"
---
# <a name="guid_ndis_enumerate_adapters_ex"></a>GUID_NDIS_ENUMERATE_ADAPTERS_EX

WMI クライアントは、GUID_NDIS_ENUMERATE_ADAPTERS_EX GUID を使用して、コンピューター上のすべてのミニポートアダプターの列挙を取得できます。 この WMI GUID は、NDIS 6.0 以降のバージョンでサポートされています。 NDIS では、読み込まれたすべてのミニポートアダプターが追跡されるため、この情報のミニポートドライバーは照会されません。

WMI クライアントは、この GUID を使用して、 [NDIS_WMI_ENUM_ADAPTER](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_enum_adapter)構造体の**netluid**メンバー内のデバイス名と関連する値を検索できます。 WMI クライアントは、その後の GUID 要求で、アダプターの**Netluid**値を使用できます。

NDIS が GUID と共に返すデータバッファーには、NDIS_WMI_ENUM_ADAPTER 構造体の配列が含まれています。

