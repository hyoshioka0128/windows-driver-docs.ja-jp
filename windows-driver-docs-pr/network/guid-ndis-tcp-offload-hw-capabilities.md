---
title: GUID_NDIS_TCP_OFFLOAD_HW_CAPABILITIES
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_TCP_OFFLOAD_HW_CAPABILITIES について説明します。
ms.assetid: 5918fcb0-ebcf-4021-99a5-9ecfd2fdb987
keywords:
- GUID_NDIS_TCP_OFFLOAD_HW_CAPABILITIES、WDK GUID_NDIS_TCP_OFFLOAD_HW_CAPABILITIES ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa475f6f64a77c8f0aea5de6104fa066c2fe9e9e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558160"
---
# <a name="guidndistcpoffloadhwcapabilities"></a>GUID_NDIS_TCP_OFFLOAD_HW_CAPABILITIES

WMI クライアントでは、ミニポート アダプターの指定したポートに関連付けられているハードウェアでサポートされている TCP オフロード機能を取得するのに GUID GUID_NDIS_TCP_OFFLOAD_HW_CAPABILITIES メソッドを使用できます。

この GUID は、NDIS ポートのハードウェア機能を返す WMI メソッド要求が必要です。 WMI のメソッド識別子は NDIS_WMI_DEFAULT_METHOD_ID、する必要があり、WMI の入力バッファーに格納する必要があります、 [NDIS_WMI_METHOD_HEADER](https://msdn.microsoft.com/library/windows/hardware/ff567903)構造体。

NDIS は、この GUID を処理し、ミニポート ドライバーが、OID クエリを受信しません。

GUID を持つ NDIS が返すデータ バッファーを含む、 [NDIS_OFFLOAD](https://msdn.microsoft.com/library/windows/hardware/ff566599)構造体。

ポートの状態の詳細については、次を参照してください。 [OID_TCP_OFFLOAD_HARDWARE_CAPABILITIES](oid-tcp-offload-hardware-capabilities.md)します。

