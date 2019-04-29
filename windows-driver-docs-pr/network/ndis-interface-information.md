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
ms.openlocfilehash: 156aaedf81de9b0b0b7cb14538ad0cc5dd7e252b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392911"
---
# <a name="ndis-interface-information"></a>NDIS インターフェイス情報





NDIS 管理情報ベース (Mib) を照会するためのインターフェイスが標準化によって、重なってドライバーとネットワーク インターフェイスに関する情報を照会ユーザー モード アプリケーションを簡単にできます。 MIB クライアントは、基になる NDIS インターフェイス プロバイダーから情報を要求する NDIS が指定した関数を呼び出します。 これにより、情報を取得する OID 要求を発行する NDIS です。 クライアントに情報を指定するには、NDIS は、NDIS を使用して、クライアントが登録されているコールバック関数を呼び出します。

NDIS ネットワーク インターフェイスのサービスの詳細については、次を参照してください。[ネットワーク インターフェイスの NDIS](https://msdn.microsoft.com/library/windows/hardware/ff566525)します。

NDIS は、強化されたサポートの Management Instrumentation (WMI) を提供します。 WMI の NDIS 6.0 のサポートの詳細については、次を参照してください。 [NDIS が WMI のサポート](ndis-support-for-wmi.md)します。

## <a name="related-topics"></a>関連トピック


[**NDIS\_インターフェイス\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff565736)

 

 






