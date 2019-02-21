---
title: 破棄の一般的な理由
description: このセクションでは、Windows Filtering Platform コールアウト ドライバーの破棄の一般的な理由について説明します。
ms.assetid: 8b2d9028-a32e-42bf-b1ba-ab029bf47d71
keywords:
- 一般的な破棄の理由によりネットワーク ドライバー
ms.date: 11/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb3fb24d49d5159a4c4b596813cd49c8d9ee08bf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527936"
---
# <a name="general-discard-reasons"></a>破棄の一般的な理由

フィルター エンジンによって、データが破棄されたことの考えられる原因の識別子は次のとおりです。 これらの識別子は、Fwpstypes.h で定義されている FWPS_GENERAL_DISCARD_REASON 列挙で定数の値です。

| 理由の識別子を破棄します。 | 理由の説明を破棄します。 |
| --- | --- |
| FWPS_DISCARD_FIREWALL_POLICY | FWP_ACTION_BLOCK アクションは、フィルター処理の決定から返されました。 |
| FWPS_DISCARD_IPSEC | 予約済み。 |

