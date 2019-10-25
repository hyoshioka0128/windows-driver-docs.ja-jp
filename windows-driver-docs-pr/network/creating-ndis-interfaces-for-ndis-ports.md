---
title: NDIS ポートの NDIS インターフェイスの作成
description: NDIS ポートの NDIS インターフェイスの作成
ms.assetid: 3a856e4d-e32a-4c8a-8fa0-9976966bdf87
keywords:
- ポート WDK NDIS、NDIS インターフェイスの作成
- NDIS ポート WDK、NDIS インターフェイスの作成
- NDIS インターフェイスプロバイダーを登録しています
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be7d5fb1b2228a7f29dd3c36e7af931451943745
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835022"
---
# <a name="creating-ndis-interfaces-for-ndis-ports"></a>NDIS ポートの NDIS インターフェイスの作成





既定では、ndis は ndis ポートの NDIS ネットワークインターフェイスを作成しません。 必要に応じて、NDIS ドライバーは[**NdisIfRegisterProvider**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterprovider)関数を呼び出して、ndis インターフェイスプロバイダーとして登録し、 [**NdisIfRegisterInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterinterface)関数を呼び出してポートのインターフェイスを登録できます。

NDIS ネットワークインターフェイスの詳細については、「 [ndis 6.0 ネットワークインターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)」を参照してください。

 

 





