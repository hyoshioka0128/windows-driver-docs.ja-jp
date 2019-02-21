---
title: I/O 要求の処理
description: I/O 要求の処理
ms.assetid: 90b1cc51-da40-45c1-9d6c-57f637f474d9
keywords:
- I/O 要求処理の WDK KMDF
- 要求オブジェクト WDK KMDF、I/O 要求の処理
- 要求の WDK KMDF、オプションの処理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95ecce43f97950304d03485a2813a4e9004af98c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56539104"
---
# <a name="processing-io-requests"></a>I/O 要求の処理





ときに、ドライバー[受信](receiving-i-o-requests.md)できますが、I/O を要求。

-   [もう一度キュー](requeuing-i-o-requests.md)別のキューに要求します。

-   [完全な](completing-i-o-requests.md)要求。

-   [キャンセル](canceling-i-o-requests.md)要求。

-   [フォワード](forwarding-i-o-requests.md)I/O のターゲットに要求します。

ドライバーを無視するか、要求を削除することはできません。

 

 





