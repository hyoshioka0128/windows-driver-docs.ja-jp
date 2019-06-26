---
title: WMI に登録されている標準ミニポート ドライバー状態表示
description: WMI に登録されている標準ミニポート ドライバー状態表示
ms.assetid: afebd0a2-c811-4534-9320-02b9292ba81b
keywords:
- 状態インジケーターの WDK ネットワー キング、WMI
- WMI の WDK は、ネットワーク状態インジケーター
- Windows Management Instrumentation WDK ネットワー キング、状態インジケーター
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a4175030b6a55869331f58ad9c0b4752d45fb8e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360760"
---
# <a name="standard-miniport-driver-status-indications-registered-with-wmi"></a>WMI に登録されている標準ミニポート ドライバー状態表示





NDIS が自動的に登録 Guid wmi のミニポート ドライバーを示す NDIS 状態インジケーターの[ **NdisMIndicateStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)または[ **NdisMCoIndicateStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismcoindicatestatusex)関数。 全般的なステータス インジケーターの一覧は、次を参照してください。[状態インジケーター](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)します。

WMI クライアント登録される WMI NDIS WMI イベントを受信すると場合、NDIS は WMI イベントに対応する NDIS 状態表示に変換し、すべてのイベントに登録されている WMI クライアントにイベントを報告します。

NDIS ドライバーは、カスタムの状態インジケーターを生成することもできます。 カスタムの状態インジケーターと WMI の詳細については、次を参照してください。 [Oid のカスタマイズと状態インジケーター](customized-oids-and-status-indications.md)します。

 

 





