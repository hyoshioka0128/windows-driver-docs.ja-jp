---
title: NDIS オブジェクト
description: NDIS オブジェクト
ms.assetid: 1a1338d7-f668-475b-99a9-4819de0a70c3
keywords:
- ジェネリックの NDIS オブジェクトの割り当てください。
- ジェネリックの NDIS オブジェクト WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a14525ed88655495c45414659fba4cc0e6393b0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354968"
---
# <a name="ndis-objects"></a>NDIS オブジェクト





使用を処理するコンポーネント、NDIS がない、 [ **NdisAllocateGenericObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisallocategenericobject)ジェネリック NDIS オブジェクトを割り当てる関数。 コンポーネントを呼び出す必要があります、 [ **NdisFreeGenericObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisfreegenericobject)関数が作成された汎用オブジェクトを解放する**NdisAllocateGenericObject**します。

汎用オブジェクトの使用方法の詳細については、次を参照してください。[プール処理を取得する](obtaining-pool-handles.md)します。

 

 





