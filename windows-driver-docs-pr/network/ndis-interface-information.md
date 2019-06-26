---
title: NDIS インターフェイス情報
description: NDIS インターフェイス情報
ms.assetid: 35187fda-a239-4801-b0be-53fcbee7d24e
keywords:
- 管理情報ベース WDK ネットワーク
- WDK のネットワー キングを (mib)
- NDIS WDK、インターフェイス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 742f31dcc55f3820ceeedf5c475d1bd945176097
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385513"
---
# <a name="ndis-interface-information"></a>NDIS インターフェイス情報





NDIS 管理情報ベース (Mib) を照会するためのインターフェイスが標準化によって、重なってドライバーとネットワーク インターフェイスに関する情報を照会ユーザー モード アプリケーションを簡単にできます。 MIB クライアントは、基になる NDIS インターフェイス プロバイダーから情報を要求する NDIS が指定した関数を呼び出します。 これにより、情報を取得する OID 要求を発行する NDIS です。 クライアントに情報を指定するには、NDIS は、NDIS を使用して、クライアントが登録されているコールバック関数を呼び出します。

NDIS ネットワーク インターフェイスのサービスの詳細については、次を参照してください。[ネットワーク インターフェイスの NDIS](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)します。

NDIS は、強化されたサポートの Management Instrumentation (WMI) を提供します。 WMI の NDIS 6.0 のサポートの詳細については、次を参照してください。 [NDIS が WMI のサポート](ndis-support-for-wmi.md)します。

## <a name="related-topics"></a>関連トピック


[**NDIS\_インターフェイス\_情報**](https://docs.microsoft.com/windows/desktop/api/ifdef/ns-ifdef-_ndis_interface_information)

 

 






