---
title: KMDF ドライバーへのアクセスの WDM インターフェイス
description: ほとんどのカーネル モード ドライバー フレームワーク (KMDF) ドライバーは、Windows Driver Model (WDM) インターフェイスに直接アクセスする必要はありません。
ms.assetid: 86e35617-cb6a-4d65-b2a6-9c7bcfa73480
keywords:
- カーネル モード ドライバー WDK KMDF、WDM
- KMDF WDK、WDM
- カーネル モード ドライバー フレームワーク、WDK WDM
- フレームワークに基づいたドライバー WDK KMDF、WDM
- WDM は、WDK KMDF をインターフェイスします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34642883ad5f0d5e4045fca6ed4b3745bfdcc419
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553932"
---
# <a name="accessing-wdm-interfaces-in-kmdf-drivers"></a>KMDF ドライバーへのアクセスの WDM インターフェイス


\[KMDF にのみ適用されます。\]

ほとんどのカーネル モード ドライバー フレームワーク (KMDF) ドライバーは、Windows Driver Model (WDM) インターフェイスに直接アクセスする必要はありません。 KMDF ドライバー WDM 情報を取得したり、IRP を操作する例については、WDM データ構造に直接アクセスを必要とする場合は、限られた状況を説明します。

## <a name="in-this-section"></a>このセクションの内容


-   [WDM 情報を取得します。](obtaining-wdm-information.md)
-   [フレームワークの外部で WDM Irp の処理](handling-wdm-irps-outside-of-the-framework.md)
-   [WDM インターフェイスの制限](wdm-interface-restrictions.md)

 

 





