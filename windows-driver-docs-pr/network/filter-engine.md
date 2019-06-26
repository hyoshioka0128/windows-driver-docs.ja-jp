---
title: フィルター エンジン
description: フィルター エンジン
ms.assetid: 87bf23c7-4086-4016-b712-a083d3d69bbe
keywords:
- フィルター エンジン WDK Windows フィルタ リング プラットフォーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6e2c1f85e6812f3c6b615376525d8db5ab8dd77
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363414"
---
# <a name="filter-engine"></a>フィルター エンジン


*フィルター エンジン*フィルターを格納し、フィルターの決定を実行する Windows フィルタ リング プラットフォームのコンポーネントです。 [フィルター](filter.md)フィルター エンジンに追加で指定された[レイヤーをフィルター処理](filtering-layer.md)フィルター エンジンは、目的のフィルター アクション (許可、drop、または引き出し) を実行できるようにします。 フィルター エンジン内のフィルターが指定されている場合、[コールアウト](callout.md)フィルターのアクションでは、フィルター エンジンの呼び出しのコールアウトの[ *classifyFn* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)吹き出しが実行できるように関数ネットワークのデータを処理します。

 

 





