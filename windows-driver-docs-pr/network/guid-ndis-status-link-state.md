---
title: GUID_NDIS_STATUS_LINK_STATE
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_STATUS_LINK_STATE について説明します。
ms.assetid: 7f56d211-14c7-4b8b-8d1c-ee7836b7b70a
keywords:
- GUID_NDIS_STATUS_LINK_STATE、WDK GUID_NDIS_STATUS_LINK_STATE ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5240daac815b7b1bc255465fd6f11c22b39b1256
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529686"
---
# <a name="guidndisstatuslinkstate"></a>GUID_NDIS_STATUS_LINK_STATE

GUID_NDIS_STATUS_LINK_STATE イベント GUID では、ミニポート アダプターのリンク状態の変更があったことを示します。 この WMI GUID は、NDIS 6.0 および以降のバージョンでサポートされます。

ミニポート ドライバーを使用して、 [NDIS_STATUS_LINK_STATE](ndis-status-link-state.md)リンクの状態に変更されたが NDIS と関連付けたドライバーに通知する状態を示す値。

ミニポート ドライバーでは、リンク状態が変化することを示します、NDIS は WMI GUID_NDIS_STATUS_LINK_STATE イベントを WMI クライアントの状態表示を変換します。

GUID を持つ NDIS を提供するデータ バッファーを含む、 [NDIS_WMI_EVENT_HEADER](https://msdn.microsoft.com/library/windows/hardware/ff567900)が続く構造体、 [NDIS_LINK_STATE](https://msdn.microsoft.com/library/windows/hardware/hh205390)構造体。 **NDIS_LINK_STATE**構造がメディアの物理的な状態を指定します。

リンクのステータスの詳細については、次を参照してください。 [OID_GEN_LINK_STATE](oid-gen-link-state.md)と[NDIS_STATUS_LINK_STATE](ndis-status-link-state.md)します。

