---
title: GUID_NDIS_GEN_PORT_AUTHENTICATION_PARAMETERS
description: このトピックでは、NDIS WMI インターフェイスの GUID を GUID_NDIS_GEN_PORT_AUTHENTICATION_PARAMETERS について説明します。
ms.assetid: a61e972b-0969-4ee8-ad57-cf88beda962d
keywords:
- GUID_NDIS_GEN_PORT_AUTHENTICATION_PARAMETERS、WDK GUID_NDIS_GEN_PORT_AUTHENTICATION_PARAMETERS ネットワーク ドライバー
ms.date: 11/22/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab1650b1f53d7feaff5eb98fef013107e77e8e18
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530796"
---
# <a name="guidndisgenportauthenticationparameters"></a>GUID_NDIS_GEN_PORT_AUTHENTICATION_PARAMETERS

WMI クライアントでは、NDIS ポートのポートの認証パラメーターを設定するのに GUID_NDIS_GEN_PORT_AUTHENTICATION_PARAMETERS セットの GUID を使用できます。 この WMI GUID は、NDIS 6.0 および以降のバージョンでサポートされます。

NDIS に変換するには、この GUID、 [OID_GEN_PORT_AUTHENTICATION_PARAMETERS](oid-gen-port-authentication-parameters.md) OID NDIS ポートの現在の認証構成を設定します。 NDIS ポートをサポートするミニポート ドライバーでは、この OID をサポートする必要があります。

WMI の入力バッファーを指定します、 [NDIS_WMI_SET_HEADER](https://msdn.microsoft.com/library/windows/hardware/ff567904) NDIS_PORT_AUTHENTICATION_PARAMETERS 構造体が続く構造体。

ポート パラメーターの詳細については、[OID_GEN_PORT_AUTHENTICATION_PARAMETERS](oid-gen-port-authentication-parameters.md)を参照してください。

