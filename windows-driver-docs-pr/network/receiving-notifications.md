---
title: 通知の受信
description: 通知の受信
ms.assetid: 852243b2-35b0-4c94-9b3b-9855ed1a678a
keywords:
- WDK ネイティブ 802.11 IHV 拡張 DLL の通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c97b6fd40e8b8f5b977ca10527c93b51bb8cccaa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385422"
---
# <a name="receiving-notifications"></a>通知の受信




 

オペレーティング システムが呼び出すことによって、ネイティブの 802.11 ミニポート ドライバーから IHV 固有の問題を転送、 [ *Dot11ExtIhvReceiveIndication* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_receive_indication)関数。 どのドライバーは、この種類を示す値の詳細については、次を参照してください。 [IHV 固有の兆候](ihv-specific-indications.md)します。

ときに、 [ *Dot11ExtIhvReceiveIndication* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wlanihv/nc-wlanihv-dot11extihv_receive_indication)関数が呼び出されると、 *pvBuffer*パラメーターには、IHV で定義された書式データが含まれているバッファーへのポインターは渡されます。

 

 





