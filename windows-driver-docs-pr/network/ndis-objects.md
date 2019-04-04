---
title: NDIS オブジェクト
description: NDIS オブジェクト
ms.assetid: 1a1338d7-f668-475b-99a9-4819de0a70c3
keywords:
- ジェネリックの NDIS オブジェクトの割り当てください。
- ジェネリックの NDIS オブジェクト WDK ネットワーク
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b67daaa31d7cbe9a46885e5799685da9cb3f0113
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557701"
---
# <a name="ndis-objects"></a>NDIS オブジェクト





使用を処理するコンポーネント、NDIS がない、 [ **NdisAllocateGenericObject** ](https://msdn.microsoft.com/library/windows/hardware/ff561603)ジェネリック NDIS オブジェクトを割り当てる関数。 コンポーネントを呼び出す必要があります、 [ **NdisFreeGenericObject** ](https://msdn.microsoft.com/library/windows/hardware/ff561850)関数が作成された汎用オブジェクトを解放する**NdisAllocateGenericObject**します。

汎用オブジェクトの使用方法の詳細については、[プール処理を取得する](obtaining-pool-handles.md)を参照してください。

 

 





