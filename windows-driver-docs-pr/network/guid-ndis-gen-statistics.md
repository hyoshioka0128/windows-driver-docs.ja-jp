---
title: GUID_NDIS_GEN_STATISTICS
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_GEN_STATISTICS について説明します。
ms.assetid: 3751d4e7-7991-4329-9eb2-6a44ca1190d4
keywords:
- GUID_NDIS_GEN_STATISTICS、WDK GUID_NDIS_GEN_STATISTICS ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd7dc45f06f5482d36d8277b1e16ee5f07407408
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325712"
---
# <a name="guidndisgenstatistics"></a>GUID_NDIS_GEN_STATISTICS

WMI クライアントは、GUID GUID_NDIS_GEN_STATISTICS メソッドを使用して、ミニポート アダプタの統計情報を取得できます。 この WMI GUID は、NDIS 6.0 および以降のバージョンでサポートされます。

WMI クライアント GUID_NDIS_GEN_STATISTICS WMI メソッドの要求を発行と NDIS ミニポート アダプターまたは NDIS ポートの現在の統計情報を返します。 WMI のメソッド識別子は NDIS_WMI_DEFAULT_METHOD_ID、する必要があり、WMI の入力バッファーに格納する必要があります、 [NDIS_WMI_METHOD_HEADER](https://msdn.microsoft.com/library/windows/hardware/ff567903)構造体。

NDIS を使用して、 [OID_GEN_STATISTICS](oid-gen-statistics.md)ミニポート アダプターの統計情報を取得する OID。 この OID は、NDIS 6.0 とそれ以降のバージョンをサポートするミニポート ドライバーに対して必須です。 統計カウンターは、符号なし 64 ビット値です。 ミニポート ドライバーでは、NDIS_STATISTICS_INFO 構造体内の統計を返します。

GUID を持つ NDIS が返すデータ バッファーには、NDIS_STATISTICS_INFO 構造体が含まれています。

