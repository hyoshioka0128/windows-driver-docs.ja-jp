---
title: コールアウト関数
description: コールアウト関数
ms.assetid: cf7b8e69-e6b2-41ac-9906-f0e3c090eb7a
keywords:
- コールアウト関数 WDK Windows フィルタリングプラットフォーム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d440d233c9988d05e8d7fdebc04afcb3d205fac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838209"
---
# <a name="callout-function"></a>コールアウト関数


コールアウト*関数*は、[コールアウトを](callout.md)定義する関数の1つである[コールアウトドライバー](callout-driver.md)によって実装される関数です。 コールアウトは、次のようなコールアウト関数の一覧で構成されています。

-   通知を処理する[*Notifyfn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_notify_fn0)関数。

-   分類を処理する[*classid*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0)関数。

-   フローの削除を処理する[*Flowdeletefn*](https://docs.microsoft.com/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_flow_delete_notify_fn0)関数 (省略可能)。

[フィルターエンジン](filter-engine.md)は、コールアウトがネットワークデータを処理できるように、コールアウトのコールアウト関数を呼び出します。

 

 





