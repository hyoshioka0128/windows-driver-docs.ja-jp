---
title: 通知の受信
description: 通知の受信
ms.assetid: 852243b2-35b0-4c94-9b3b-9855ed1a678a
keywords:
- 通知 WDK ネイティブ 802.11 IHV Extensions DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 567766b766b06467ff7c4bb875b54fc1ca4bbe5b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842102"
---
# <a name="receiving-notifications"></a>通知の受信




 

オペレーティングシステムは、 [*Dot11ExtIhvReceiveIndication*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_indication)関数を呼び出すことによって、ネイティブ802.11 ミニポートドライバーから IHV 固有の指示を転送します。 ドライバーがこの種の説明を行う方法の詳細については、「 [IHV 固有](ihv-specific-indications.md)の表示」を参照してください。

[*Dot11ExtIhvReceiveIndication*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_indication)関数が呼び出されると、 *pvbuffer*パラメーターには、IHV によって定義された形式のデータを格納するバッファーへのポインターが渡されます。

 

 





