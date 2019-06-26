---
title: コールアウト関数
description: コールアウト関数
ms.assetid: cf7b8e69-e6b2-41ac-9906-f0e3c090eb7a
keywords:
- 吹き出し関数 WDK Windows フィルタ リング プラットフォーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a64682863c16ba3aa111bf1710e1c1b5b6d98245
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382809"
---
# <a name="callout-function"></a>コールアウト関数


A*コールアウト関数*によって実装されている関数には、[コールアウト ドライバー](callout-driver.md)を定義する関数の 1 つは、[コールアウト](callout.md)。 コールアウトは、引き出し関数の次の一覧で構成されます。

-   A [ *notifyFn* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nc-fwpsk-fwps_callout_notify_fn0)通知を処理する関数。

-   A [ *classifyFn* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)プロセス分類する関数。

-   A [ *flowDeleteFn* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/fwpsk/nc-fwpsk-fwps_callout_flow_delete_notify_fn0)関数をプロセス フローの削除 (省略可能)。

[フィルター エンジン](filter-engine.md)コールアウトは、ネットワークのデータを処理できるように吹き出しのコールアウトが関数の呼び出し。

 

 





