---
title: パラレル ポートとデバイスのデバイス スタック
description: パラレル ポートとデバイスのデバイス スタック
ms.assetid: 80222ed9-f900-4d97-b459-2d8ca780e1d1
keywords:
- システム提供平行ドライバー WDK、デバイス スタック
- デバイス履歴の WDK 並列ドライバー
- デバイス WDK、デバイス スタックを並列します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ec93a7c51fef316270e256b381e2ec20916ee4a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376966"
---
# <a name="device-stacks-for-parallel-ports-and-devices"></a>パラレル ポートとデバイスのデバイス スタック





このセクションでは、パラレル ポートおよびパラレル ポートに接続されているデバイスのシステム提供平行ドライバーによって作成されたデバイス スタックについて説明します。

次の図は、パラレル ポートおよびパラレル ポートに接続されたデバイスのシステム提供平行ドライバーを作成するデバイス スタックの種類を示します。

![パラレル ポートやデバイスの windows デバイスとドライバー スタックを示す図](images/parport4.png)

パラレル ポートに接続されている並列のデバイス用のドライバーのベンダーによって提供される関数は省略可能です。 システム提供平行ドライバー提供広範なサポート、ロウ デバイスとしての並列のデバイスを直接制御するため、デバイスの親を制御するためパラレル ポート。

パラレル ポートおよびパラレル ポートに接続されているデバイスが動作する方法の詳細についてを参照してください。

[並列デバイス インターフェイス、内部名は、シンボリック リンク](parallel-device-interfaces--internal-names--and-symbolic-links.md)

[IOCTL およびパラレル ポートとデバイスのコールバック サポート](ioctl-and-callback-support-for-parallel-ports-and-devices.md)

[パラレル ポートの動作](operating-a-parallel-port.md)

[パラレル ポートに接続されている並列のデバイスの動作](operating-a-parallel-device-attached-to-a-parallel-port.md)

[システム提供平行ドライバーへのクライアント インターフェイス](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)

 

 




