---
title: 中間ドライバーでの状態表示
description: 中間ドライバーでの状態表示
ms.assetid: be8d50f9-4a8d-4f3c-a507-e64dedff9a3e
keywords:
- 中間ドライバー WDK ネットワー キング、状態インジケーター
- NDIS 中間ドライバー WDK、状態インジケーター
- 状態インジケーター WDK、中間ネットワーク ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2903f03f0ba1ad5844a7c20b955911c0b17220c2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580333"
---
# <a name="status-indications-in-an-intermediate-driver"></a>中間ドライバーでの状態表示





中間ドライバーで状態インジケーターの実装では、プロトコル ドライバーに実装するとほぼ同じです。 ドライバーの中間状態のインジケーターの詳細については、次を参照してください。[プロトコル ドライバーに状態インジケーター](status-indications-in-a-protocol-driver.md)します。

呼び出すことによってより高度なドライバーまで、状態を示す値を示している可能性、中間ドライバーでは、状態を示す値を受信すると[ **NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)します。 中間のドライバーには、その特定のデザイン要件に合わせて上にあるドライバーへの状態の変更が示されます。

 

 





