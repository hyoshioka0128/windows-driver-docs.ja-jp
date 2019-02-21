---
title: GUID_NDIS_GEN_LINK_STATE
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_GEN_LINK_STATE について説明します。
ms.assetid: 0b0ebb57-33fb-4a18-b6e5-3f4300729280
keywords:
- GUID_NDIS_GEN_LINK_STATE、WDK GUID_NDIS_GEN_LINK_STATE ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa0c54c0e7f15bd691bfe3d1ed5e72a969144339
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527385"
---
# <a name="guidndisgenlinkstate"></a>GUID_NDIS_GEN_LINK_STATE

WMI クライアントでは、現在のリンクの状態を判断するのに GUID_NDIS_GEN_LINK_STATE メソッド GUID を使用できます。 この WMI GUID は、NDIS 6.0 および以降のバージョンでサポートされます。

NDIS は、この GUID を処理し、ミニポート ドライバーが、OID クエリを受信しません。

WMI クライアント GUID_NDIS_GEN_LINK_STATE WMI メソッドの要求を発行と NDIS ミニポート アダプターまたは NDIS ポートの現在のリンクの状態を返します。

WMI のメソッド識別子は NDIS_WMI_DEFAULT_METHOD_ID、する必要があり、WMI の入力バッファーに格納する必要があります、 [NDIS_WMI_METHOD_HEADER](https://msdn.microsoft.com/library/windows/hardware/ff567903)構造体。

この GUID を持つ NDIS が返すデータ バッファーを含む、 [NDIS_LINK_STATE](https://msdn.microsoft.com/library/windows/hardware/hh205390)構造体。

ミニポート ドライバーでは、初期化中に、リンクの状態を指定し、状態インジケーターの更新プログラムを提供します。 WMI クライアントでは、リンクの状態が変更されたときに、更新プログラムを受信するのに GUID_NDIS_GEN_LINK_STATE GUID を使用できます。

リンクのステータスの詳細については、次を参照してください。 [OID_GEN_LINK_STATE](oid-gen-link-state.md)と[NDIS_STATUS_LINK_STATE](ndis-status-link-state.md)します。

