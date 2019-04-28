---
title: ドライバーでの PnP と電源管理のサポート
description: ドライバーでの PnP と電源管理のサポート
ms.assetid: d9cf987f-d994-4ea9-a467-4b1b8bcdc456
keywords:
- WDK KMDF の PnP、約 framework ベースのドライバーの PnP
- プラグ アンド プレイ WDK KMDF は、約 framework ベースのドライバーの PnP します。
- 電源管理 WDK KMDF、電源管理について
- デバイス オブジェクト WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27ac07be5276d71a53713c9d7845e291903e73f5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380498"
---
# <a name="supporting-pnp-and-power-management-in-your-driver"></a>ドライバーでの PnP と電源管理のサポート


既定では、フレームワークは、システムが framework ベースのドライバーに送信するすべての PnP や電源管理要求を処理します。 さらに、既定では、フレームワークの I/O 要求を配信関数ドライバー、ドライバーのハードウェアが使用可能で、作業 (D0) 状態の場合にのみ。

フレームワーク ベースのドライバーを記述する場合は、簡単にデバイスの PnP や電源管理機能をサポートするために、フレームワークの既定の動作の多くを使用できます。 ただし、すべてのドライバーがドライバー スタックは、フレームワークの既定の PnP や電源管理動作のみを使用する場合、デバイスおそらくは正しく機能しません。 たとえば、デバイスの機能のドライバーでは、デバイスがその作業 (D0) 状態に入ったときに、デバイスを有効にする必要があります。

したがって、framework デバイス オブジェクトは、一連のイベントのコールバック関数を提供します。、PnP ドライバー パッケージと電源管理操作に参加するフレームワーク ベースのドライバーを有効にするオブジェクトのメソッドのセット。 これらのコールバック関数とオブジェクトのメソッドは、各ドライバーのみ PnP を提供するスタックと必要な電源管理のサポートを許可します。

通常、ドライバー スタックのさまざまなドライバーの各はいくつかの PnP、電源管理操作のサポートを担当します。 ドライバーがサポートする操作は、作成しているドライバーとデバイスが用意されている機能の種類によって異なります。 操作の詳細については、ドライバーはサポートする必要がありますを参照してください。

-   [ソフトウェア専用のドライバーでの PnP や電源管理のサポート](supporting-pnp-and-power-management-in-software-only-drivers.md)
-   [関数のドライバーでの PnP や電源管理のサポート](supporting-pnp-and-power-management-in-function-drivers.md)

 

 





