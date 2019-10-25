---
title: NDIS オブジェクト
description: NDIS オブジェクト
ms.assetid: 1a1338d7-f668-475b-99a9-4819de0a70c3
keywords:
- 汎用 NDIS オブジェクトの割り当て
- 汎用 NDIS オブジェクト WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80d506f8a3a2644e3fa014b5777b010379769290
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844359"
---
# <a name="ndis-objects"></a>NDIS オブジェクト





NDIS ハンドルを持たないコンポーネントでは、 [**NdisAllocateGenericObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisallocategenericobject)関数を使用して、汎用の NDIS オブジェクトを割り当てます。 コンポーネントは、 **NdisAllocateGenericObject**で作成された汎用オブジェクトを解放するために、 [**NdisFreeGenericObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisfreegenericobject)関数を呼び出す必要があります。

ジェネリックオブジェクトの使用方法の詳細については、「[プールハンドルの取得](obtaining-pool-handles.md)」を参照してください。

 

 





