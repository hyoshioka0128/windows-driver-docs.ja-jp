---
title: NdisXxx 関数への呼び出しの違い
description: NdisXxx 関数への呼び出しの違い
ms.assetid: 967ad913-24ca-4f05-b10b-1daa88845ed3
keywords:
- NdisCmXxx 関数 WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e60f11be0dba00b38df3876e4cd53ea46dce6924
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532811"
---
# <a name="differences-in-calls-to-ndisxxx-functions"></a>NdisXxx 関数への呼び出しの違い





コール マネージャーは、さまざまな呼び出しにより、MCM ドライバー マネージャーの機能を呼び出します。 コール マネージャーを呼び出す**NdisCm * Xxx*** 関数、および、MCM ドライバー呼び出し**NdisMCm * Xxx*** 関数。

MCM にドライバーを呼び出しません、 **NdisCo * Xxx*** クライアントの接続指向とコール マネージャーの両方を呼び出す関数。 代わりに、MCM、ドライバーを呼び出す次同等**NdisMCm * Xxx*** 関数。

-   [**NdisMCmCreateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff562812)の代わりに[ **NdisCoCreateVc**](https://msdn.microsoft.com/library/windows/hardware/ff561696)

-   [**NdisMCmDeleteVc** ](https://msdn.microsoft.com/library/windows/hardware/ff562819)の代わりに[ **NdisCoDeleteVc**](https://msdn.microsoft.com/library/windows/hardware/ff561698)

-   [**NdisMCmOidRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff563548)の代わりに[ **NdisCoOidRequest**](https://msdn.microsoft.com/library/windows/hardware/ff561711)

-   [**NdisMCmOidRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff563551)の代わりに[ **NdisCoOidRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff561716)

MCM にドライバーに匹敵する呼び出しが不要[ **NdisCoSendNetBufferLists**](https://msdn.microsoft.com/library/windows/hardware/ff561728)コール マネージャーとミニポート ドライバー間の送信インターフェイスは、MCM ドライバーに内部であるため、NDIS したがって不透明になります。

 

 





