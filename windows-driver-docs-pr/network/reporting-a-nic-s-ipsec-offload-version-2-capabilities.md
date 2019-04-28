---
title: NIC の IPsec Offload Version 2 の機能のレポート
description: NIC の IPsec Offload Version 2 の機能のレポート
ms.assetid: 0ce5c42d-5c0c-4dfa-8a9f-a80c8924201d
keywords:
- IPsecOV2 WDK TCP/IP トランスポート、機能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 024c6181c96cd3a775b8e72c3b987303aee4fa3e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380878"
---
# <a name="reporting-a-nics-ipsec-offload-version-2-capabilities"></a>NIC の IPsec Offload Version 2 の機能のレポート

\[IPsec タスク オフロード機能は非推奨し、は使用できません。\]




IPsec オフロード バージョン 2 (IPsecOV2) を指定する、現在、NDIS 6.1 と以降のバージョンのミニポート ドライバー、機能するを指定しますまたは既定の構成では、NIC の、 [ **NDIS\_IPSEC\_オフロード\_V2。** ](https://msdn.microsoft.com/library/windows/hardware/ff565808)構造体。 ミニポート ドライバーが既定の IPsecOV2 構成を含める必要があります、 [ **NDIS\_ミニポート\_アダプター\_オフロード\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff565930)構造体。 ミニポート ドライバーの呼び出し、 [ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)関数を[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)関数を渡す、NDIS 情報\_ミニポート\_アダプター\_オフロード\_属性。

ミニポート ドライバーが存在する場合に IPsecOV2 機能、変更を報告する必要がありますで、 [ **NDIS\_状態\_タスク\_オフロード\_現在\_CONFIG**](https://msdn.microsoft.com/library/windows/hardware/ff567424)状態を示す値。

**注**  NDIS NDIS 6.1 と以降のドライバーの直接の OID 要求インターフェイスを提供します。 [OID の直接の要求パス](https://msdn.microsoft.com/library/windows/hardware/ff564736)クエリを実行したり、頻繁に設定されている OID 要求をサポートします。

 

クエリに対する応答で[OID\_TCP\_オフロード\_現在\_CONFIG](https://msdn.microsoft.com/library/windows/hardware/ff569805)、NDIS には、NDIS が含まれています\_IPSEC\_オフロード\_V2構造体、 [ **NDIS\_オフロード**](https://msdn.microsoft.com/library/windows/hardware/ff566599) NDIS を表す構造体、 **InformationBuffer**のメンバー、 [ **NDIS\_OID\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff566710)構造体。 NDIS は、ミニポート ドライバーが提供される情報を使用します。

 

 





