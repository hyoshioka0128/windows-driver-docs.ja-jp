---
title: WMI に登録されている標準ミニポート ドライバー OID
description: WMI に登録されている標準ミニポート ドライバー OID
ms.assetid: 87529f7f-8d62-4067-b008-7c4a04d7a7c6
keywords:
- ミニポート アダプタの WDK ネットワー キング、WMI
- アダプターの WDK ネットワー キング、WMI
- WMI の WDK にネットワーク接続、Oid
- Oid WDK ネットワー キング、WMI
- Windows Management Instrumentation の WDK ネットワー キング、Oid
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49aa0f1f5e6be80049d5d6d60975f3c0f789710c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346013"
---
# <a name="standard-miniport-driver-oids-registered-with-wmi"></a>WMI に登録されている標準ミニポート ドライバー OID





NDIS は、ミニポート アダプターの WMI で WMI の Guid を登録します。 Oid ミニポート アダプターがサポートする NDIS 問題の一覧を取得する、 [OID\_GEN\_サポートされている\_一覧](https://msdn.microsoft.com/library/windows/hardware/ff569642)が関連付けられているミニポート ドライバーにクエリします。 ミニポート ドライバーには、ミニポート アダプターをサポートする Oid のすべての一覧を指定する必要があります。 この一覧は、すべての必須の Oid を含める必要があり、存在する場合、省略可能で、カスタムの Oid を含める必要があります。

NDIS は、サポートされている Oid を WMI Guid にマップされ、Guid を WMI に登録されます。 NDIS は、必要に応じて、登録済みの Oid の OID の要求に GUID の WMI 要求を変換します。

NDIS ドライバーでは、WMI でカスタム Guid を登録することもできます。 詳細については、カスタム Guid は、次を参照してください。 [Oid のカスタマイズと状態インジケーター](customized-oids-and-status-indications.md)します。

NDIS は、WMI イベントに状態インジケーターにも変換します。 WMI イベントに状態インジケーターの翻訳の詳細については、次を参照してください。[標準ミニポート ドライバーの状態に登録されている WMI](standard-miniport-driver-status-indications-registered-with-wmi.md)します。

 

 





