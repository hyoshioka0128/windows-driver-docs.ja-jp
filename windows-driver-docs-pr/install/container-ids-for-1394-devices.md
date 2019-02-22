---
title: 1394 デバイス用のコンテナー Id
description: 1394 デバイス用のコンテナー Id
ms.assetid: 667df2c6-bbbd-41da-b626-da493e316016
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1ef0e397ed3eb916529c8623d795dc3d1f20dfb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56530415"
---
# <a name="container-ids-for-1394-devices"></a>1394 デバイス用のコンテナー Id


1394 のバス仕様では、デバイス関数は、またはは、1394 ホスト コント ローラーから削除できないかどうかを示す、内部ハードウェア メカニズムは指定しません。 Windows に含まれている 1394 バス ドライバーは、デバイスのすべてのノードをマーク (*devnode*)、親ホスト コント ローラーからリムーバブルとします。

1 つの 1394 デバイスは、複数のデバイス機能を公開する場合、バス ドライバーを列挙する各 devnode はリムーバブルとマークされます。 ただし、Windows に含まれている 1394 バス ドライバーが認識できるは、各 devnode が 1 台のデバイスから発生し、各 devnode に同じコンテナー ID を割り当てます。 そのため、各 1394 デバイスは、1 つのデバイス コンテナー オブジェクトを受け取るし、デバイスとプリンターのユーザー インターフェイス (UI) で 1 つのデバイスとして表示されます。

 

 





