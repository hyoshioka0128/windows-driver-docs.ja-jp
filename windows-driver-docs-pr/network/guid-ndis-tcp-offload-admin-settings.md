---
title: GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS について説明します。
ms.assetid: 8648c75a-dcb3-4723-a2d0-d406d3a073d6
keywords:
- GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS、WDK GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e530dc8b9645ec1ef24e7cd62df37316e830c2a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579822"
---
# <a name="guidndistcpoffloadadminsettings"></a>GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS

WMI クライアントでは、オフロードは、NDIS ポートの構成パラメーターを設定するのに GUID_NDIS_TCP_OFFLOAD_ADMIN_SETTINGS セットの GUID を使用できます。 この WMI GUID は、NDIS 6.0 および以降のバージョンでサポートされます。

NDIS に変換するには、この GUID、 [OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md) NDIS ポートの現在の構成を設定する OID。 タスク オフロードの任意の種類のサポートを提供する NDIS ミニポート ドライバーでは、この OID をサポートする必要があります。

WMI の入力バッファーが含まれています、 [NDIS_WMI_SET_HEADER](https://msdn.microsoft.com/library/windows/hardware/ff567904)が続く構造体、 [NDIS_OFFLOAD_PARAMETERS](https://msdn.microsoft.com/library/windows/hardware/ff566706)構造体。

ポート パラメーターの詳細については、次を参照してください。 [OID_TCP_OFFLOAD_PARAMETERS](oid-tcp-offload-parameters.md)します。

