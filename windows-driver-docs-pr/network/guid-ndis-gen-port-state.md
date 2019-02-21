---
title: GUID_NDIS_GEN_PORT_STATE
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_GEN_PORT_STATE について説明します。
ms.assetid: 0632843e-ea79-4ada-919e-8ab7d94a4421
keywords:
- GUID_NDIS_GEN_PORT_STATE、WDK GUID_NDIS_GEN_PORT_STATE ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2909886d1406b833e5926535e4ceeac812ad1a3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549270"
---
# <a name="guidndisgenportstate"></a>GUID_NDIS_GEN_PORT_STATE

WMI クライアントでは、NDIS ポートの状態を取得するのに GUID GUID_NDIS_GEN_PORT_STATE メソッドを使用できます。 この WMI GUID は、NDIS 6.0 および以降のバージョンでサポートされます。

GUID_NDIS_GEN_PORT_STATE では、NDIS ポートの状態を返す WMI メソッド要求が必要です。 WMI のメソッド識別子は NDIS_WMI_DEFAULT_METHOD_ID、する必要があり、WMI の入力バッファーに格納する必要があります、 [NDIS_WMI_METHOD_HEADER](https://msdn.microsoft.com/library/windows/hardware/ff567903)構造体。

NDIS は、この GUID を処理し、ミニポート ドライバーが、OID クエリを受信しません。

GUID を持つ NDIS が返すデータ バッファーを含む、 [NDIS_PORT_STATE](https://msdn.microsoft.com/library/windows/hardware/ff569624)構造体。

ポートの状態の詳細については、次を参照してください。 [OID_GEN_PORT_STATE](oid-gen-port-state.md)します。

