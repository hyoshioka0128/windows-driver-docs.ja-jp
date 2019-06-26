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
ms.openlocfilehash: b8086afd731fe3c07aae924c0040f90e610a12d9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374895"
---
# <a name="creating-ndis-interfaces-for-ndis-ports"></a>NDIS ポートの NDIS インターフェイスの作成





既定では、NDIS で NDIS ポートの NDIS ネットワーク インターフェイスが作成されることはできません。 かどうか必要に応じて、NDIS ドライバーを呼び出して、 [ **NdisIfRegisterProvider** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifregisterprovider) NDIS インターフェイス プロバイダーの呼び出しとして登録する関数、 [ **NdisIfRegisterInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisifregisterinterface)ポートのインターフェイスを登録する関数。

NDIS ネットワーク インターフェイスの詳細については、次を参照してください。 [NDIS 6.0 のネットワーク インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)します。

 

 





