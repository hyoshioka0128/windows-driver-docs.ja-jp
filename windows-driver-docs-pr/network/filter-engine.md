---
title: フィルター エンジン
description: フィルター エンジン
ms.assetid: 87bf23c7-4086-4016-b712-a083d3d69bbe
keywords:
- フィルター エンジン WDK Windows フィルタ リング プラットフォーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9b66cd33d868881790bb538310ca6524e77f0ff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529485"
---
# <a name="filter-engine"></a>フィルター エンジン


*フィルター エンジン*フィルターを格納し、フィルターの決定を実行する Windows フィルタ リング プラットフォームのコンポーネントです。 [フィルター](filter.md)フィルター エンジンに追加で指定された[レイヤーをフィルター処理](filtering-layer.md)フィルター エンジンは、目的のフィルター アクション (許可、drop、または引き出し) を実行できるようにします。 フィルター エンジン内のフィルターが指定されている場合、[コールアウト](callout.md)フィルターのアクションでは、フィルター エンジンの呼び出しのコールアウトの[ *classifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff544890)吹き出しが実行できるように関数ネットワークのデータを処理します。

 

 





