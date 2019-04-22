---
title: PnP と電源管理のコールバック シーケンス
description: 次のトピックで、フレームワーク、WDF ドライバーの PnP シーケンスと電源管理イベントのコールバック関数を説明します。
ms.assetid: 74663110-8E3C-4AC4-8BCD-63C788047F38
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3fa9d5546027d1509266eee098024c1af27c52ce
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/18/2019
ms.locfileid: "58761839"
---
# <a name="pnp-and-power-management-callback-sequences"></a>PnP と電源管理のコールバック シーケンス


次のトピックでは、シーケンスをフレームワーク (KMDF および UMDF v2) の WDF ドライバーの PnP と電源管理イベントのコールバック関数を示しています。

-   [関数またはフィルター ドライバーの電源投入シーケンス](power-up-sequence-for-a-function-or-filter-driver.md)
-   [バス ドライバーの電源投入シーケンス](power-up-sequence-for-a-bus-driver.md)
-   [電源と関数、またはフィルター ドライバーの削除順序](power-down-and-removal-sequence-for-a-function-or-filter-driver.md)
-   [電源とバス ドライバーの削除順序](power-down-and-removal-sequence-for-a-bus-driver.md)
-   [シーケンスの突然の取り外し](surprise-removal-sequence.md)
-   [WDM Irp と対応する WDF イベントのコールバック](https://docs.microsoft.com/windows-hardware/drivers/wdf/wdm-irps-and-kmdf-event-callback-functions)

次のトピックでは、PnP、電源管理の一般的なシナリオを特定し、これで、フレームワーク ドライバーのイベントのコールバック関数これらのシナリオの中に、シーケンスを表示します。

- [ユーザーはデバイスをプラグインします。](a-user-plugs-in-a-device.md)
- [ユーザーがデバイスから切り離し](a-user-unplugs-a-device.md)
- [デバイスが省電力状態に入る](a-device-enters-a-low-power-state.md)
- [デバイスは、作業の状態に戻ります](a-device-returns-to-its-working-state.md)
- [PnP マネージャーでシステム リソースを再配布します。](the-pnp-manager-redistributes-system-resources.md)
 

 





