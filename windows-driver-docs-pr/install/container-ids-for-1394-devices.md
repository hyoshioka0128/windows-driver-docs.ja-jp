---
title: 1394 デバイス用のコンテナー ID
description: 1394 デバイス用のコンテナー ID
ms.assetid: 667df2c6-bbbd-41da-b626-da493e316016
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c1ef0e397ed3eb916529c8623d795dc3d1f20dfb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346854"
---
# <a name="container-ids-for-1394-devices"></a>1394 デバイス用のコンテナー ID


1394 のバス仕様では、デバイス関数は、またはは、1394 ホスト コント ローラーから削除できないかどうかを示す、内部ハードウェア メカニズムは指定しません。 Windows に含まれている 1394 バス ドライバーは、デバイスのすべてのノードをマーク (*devnode*)、親ホスト コント ローラーからリムーバブルとします。

1 つの 1394 デバイスは、複数のデバイス機能を公開する場合、バス ドライバーを列挙する各 devnode はリムーバブルとマークされます。 ただし、Windows に含まれている 1394 バス ドライバーが認識できるは、各 devnode が 1 台のデバイスから発生し、各 devnode に同じコンテナー ID を割り当てます。 そのため、各 1394 デバイスは、1 つのデバイス コンテナー オブジェクトを受け取るし、デバイスとプリンターのユーザー インターフェイス (UI) で 1 つのデバイスとして表示されます。

 

 





