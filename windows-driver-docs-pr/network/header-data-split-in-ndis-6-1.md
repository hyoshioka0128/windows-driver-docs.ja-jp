---
title: NDIS 6.1 でヘッダー データの分割
description: NDIS 6.1 でヘッダー データの分割
ms.assetid: f4380956-b18b-46f4-9c2e-d8124cbf5c3f
keywords:
- ヘッダー データ ヘッダー データの分割について、WDK を分割します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3fcabef751fc85b7ed56c92bfc0fe79fcd9cede
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551034"
---
# <a name="header-data-split-in-ndis-61"></a>NDIS 6.1 でヘッダー データの分割





*ヘッダー データが分割*サービスを別のバッファーにヘッダーと受信のイーサネット フレーム内のデータを分割することでネットワーク パフォーマンスが向上します。 ヘッダーと、データ、分離してこれらのサービスには、メモリの領域が小さい方にまとめて収集するヘッダーが有効にします。 したがって、追加のヘッダーが 1 つのメモリ ページに収まるとシステム キャッシュに追加のヘッダーに合わせてでメモリのオーバーヘッドにアクセスするため、ドライバー スタックが削減されます。

ヘッダー データの分割インターフェイスは、ヘッダーにデータの分割に対応したネットワーク インターフェイス カード (Nic) の提供される省略可能なサービスです。

ヘッダー データの分割の詳細については、[ヘッダー データの分割](header-data-split.md)を参照してください。

 

 





