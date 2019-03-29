---
title: NDIS ポートの NDIS インターフェイスの作成
description: NDIS ポートの NDIS インターフェイスの作成
ms.assetid: 3a856e4d-e32a-4c8a-8fa0-9976966bdf87
keywords:
- ポートの WDK NDIS、NDIS インターフェイスを作成します。
- NDIS ポート WDK、NDIS を作成するインターフェイスします。
- NDIS インターフェイス プロバイダーを登録します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d223278d2dde8313dbeca5238d8649bde0bcafa5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579456"
---
# <a name="creating-ndis-interfaces-for-ndis-ports"></a>NDIS ポートの NDIS インターフェイスの作成





既定では、NDIS で NDIS ポートの NDIS ネットワーク インターフェイスが作成されることはできません。 かどうか必要に応じて、NDIS ドライバーを呼び出して、 [ **NdisIfRegisterProvider** ](https://msdn.microsoft.com/library/windows/hardware/ff562716) NDIS インターフェイス プロバイダーの呼び出しとして登録する関数、 [ **NdisIfRegisterInterface**](https://msdn.microsoft.com/library/windows/hardware/ff562715)ポートのインターフェイスを登録する関数。

NDIS ネットワーク インターフェイスの詳細については、次を参照してください。 [NDIS 6.0 のネットワーク インターフェイス](https://msdn.microsoft.com/library/windows/hardware/ff566525)します。

 

 





