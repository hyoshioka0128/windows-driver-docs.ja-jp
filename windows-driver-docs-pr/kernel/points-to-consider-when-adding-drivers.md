---
title: ドライバーを追加するときに考慮すべき点
description: ドライバーを追加するときに考慮すべき点
ms.assetid: bcbaa842-03b6-4311-9b93-1a4af165020b
keywords:
- WDM ドライバー WDK カーネルの構成
- WDM ドライバー WDK カーネル、複数層のドライバー
- 階層型ドライバー WDK カーネル
- ドライバーは、WDK WDM をレイヤーします。
- ドライバーの置き換え
- カーネル モード ドライバーを追加します。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49c29a60fd6065c5bdd2048c69c24a273f168eb9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56559054"
---
# <a name="points-to-consider-when-adding-drivers"></a>ドライバーを追加するときに考慮すべき点





カーネル モード ドライバーを設計するときに、次の点に注意してくださいにしてください。

-   システム提供の SCSI とビデオ ポート ドライバーを置き換えることができません。

-   代替最下位レベルのドライバーでは、置換ドライバーと同じ機能を実装する必要があります。 代替キーボードまたはマウス ポート ドライバーが自体と再利用するは、システム指定のクラス ドライバーのシステム定義インターフェイスを使用する必要がありますなど、その逆です。

-   上限と下限のドライバーの機能が制限しないようにそれらのドライバーとドライバーのシステム提供のペアの間に挿入される新しい中間ドライバーの相互運用する必要があります。

 

 




