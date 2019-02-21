---
title: 通知の受信
description: 通知の受信
ms.assetid: 852243b2-35b0-4c94-9b3b-9855ed1a678a
keywords:
- WDK ネイティブ 802.11 IHV 拡張 DLL の通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa03f6d5fa841fd7c0e7efc8d616cf2069e1f147
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553514"
---
# <a name="receiving-notifications"></a>通知の受信




 

オペレーティング システムが呼び出すことによって、ネイティブの 802.11 ミニポート ドライバーから IHV 固有の問題を転送、 [ *Dot11ExtIhvReceiveIndication* ](https://msdn.microsoft.com/library/windows/hardware/ff547512)関数。 どのドライバーは、この種類を示す値の詳細については、次を参照してください。 [IHV 固有の兆候](ihv-specific-indications.md)します。

ときに、 [ *Dot11ExtIhvReceiveIndication* ](https://msdn.microsoft.com/library/windows/hardware/ff547512)関数が呼び出されると、 *pvBuffer*パラメーターには、IHV で定義された書式データが含まれているバッファーへのポインターは渡されます。

 

 





