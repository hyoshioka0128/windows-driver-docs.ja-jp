---
title: フィルター エンジン
description: フィルター エンジン
ms.assetid: 87bf23c7-4086-4016-b712-a083d3d69bbe
keywords:
- フィルターエンジン WDK Windows フィルタリングプラットフォーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85a876b83206b0285f12054b8f8399f951c5977c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834710"
---
# <a name="filter-engine"></a>フィルター エンジン


*フィルターエンジン*は、フィルターを格納し、フィルターの決定を実行する Windows フィルタリングプラットフォームのコンポーネントです。 フィルターは、フィルターエンジンが目的のフィルター処理 (許可、削除、またはコールアウト) を実行できるように、指定された[フィルターレイヤー](filtering-layer.md)のフィルターエンジンに追加[されます](filter.md)。 フィルターエンジンのフィルターによってフィルターのアクションの[コールアウト](callout.md)が指定されている場合、フィルターエンジンはコールアウトの[*classid*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)関数を呼び出して、コールアウトがネットワークデータを処理できるようにします。

 

 





