---
title: WDM デバイス オブジェクトを作成する場合
description: WDM デバイス オブジェクトを作成する場合
ms.assetid: aeb8039d-2e5d-4700-a9e5-e5ee97c6b0b1
keywords:
- 作成されたときにデバイス オブジェクト WDK カーネル
- 階層型のデバイス オブジェクトの WDK カーネル
- 機能のデバイス オブジェクトの WDK カーネル
- FDO WDK カーネル
- 物理デバイス オブジェクトの WDK カーネル
- Pdo WDK カーネル
- フィルター DOs WDK カーネル
- デバイス履歴の WDK カーネル、デバイス オブジェクト レイヤーが可能
- デバイス オブジェクトのアタッチ
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ed3b8b263e8997a5175d4ef3f29c0a84fe25d84
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358107"
---
# <a name="when-are-wdm-device-objects-created"></a>WDM デバイス オブジェクトが作成される場合





このセクションでは、デバイス オブジェクトの種類ごとの説明し、それぞれが作成されるときにメンションします。

次の図は、デバイス スタック、デバイスの I/O 要求を処理してドライバーを表す接続できるデバイス オブジェクトの可能な種類を示します。

![デバイスのデバイス オブジェクト レイヤーを示す図](images/objlyr.png)

この図の下部にある開始。

-   バス ドライバー、バスが列挙される各デバイスの PDO を作成します。

    バス ドライバーは、デバイスを列挙したときに子デバイス用の PDO を作成します。 バス ドライバーへの応答内のデバイスの列挙、 [ **IRP\_MN\_クエリ\_デバイス\_リレーション**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-device-relations)要求**BusRelations** PnP マネージャーから。 クエリ リレーションシップの要求に応答した子デバイスが最後に、バス ドライバー、バスにデバイスが追加されている場合のバス ドライバーは、PDO を作成します**BusRelations** (または以降の最初のクエリ関係要求の場合、。マシンは起動でした)。

    PDO は、電源マネージャー、PnP マネージャーでは、I/O マネージャーなどの他のカーネル モードのシステム コンポーネントのほか、バス ドライバーにデバイスを表します。

    その他のドライバー、デバイス接続、PDO が PDO の上にデバイス オブジェクトは常にデバイス スタックの下部にあります。

-   省略可能な bus フィルター ドライバーは、各デバイスのフィルター DOs を作成します。

    PnP マネージャーがで新しいデバイスを検出した場合、 **BusRelations**一覧で、デバイスのバス フィルター ドライバーがあるかどうかが決定します。 場合、そのため、このような各ドライバーの PnP マネージャーによりが読み込まれる (呼び出し[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)必要な場合)、ドライバーの呼び出しと[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)ルーチン。 フィルター ドライバーがデバイス オブジェクトを作成しでデバイス スタックに接続される場合は、bus フィルター ドライバーは、このデバイスの操作をフィルター処理、その*AddDevice*ルーチン。 1 つ以上のバス フィルター ドライバーが存在し、このデバイスに関連する、各フィルター ドライバーは作成し、独自のデバイス オブジェクトをアタッチします。

-   省略可能な低レベルのフィルター ドライバーは、各デバイスのフィルター DOs を作成します。

    省略可能、下位レベルのフィルター ドライバーは、このデバイスの存在、PnP マネージャーにより、バス ドライバー、バス フィルター ドライバーの後にこのようなドライバーが読み込まれているようになります。 PnP マネージャーには、フィルター ドライバーの*AddDevice*ルーチン。 その*AddDevice* 、日常的な下位レベルのフィルター ドライバー、デバイスのフィルター操作を実行を作成し、デバイス スタックを結び付けます。 1 つ以上の下位レベルのフィルター ドライバーが存在する場合、このような各ドライバーは作成し、独自のフィルター操作をアタッチします。

-   関数のドライバーでは、デバイスの FDO を作成します。

    PnP マネージャーにより、デバイスの機能のドライバーが読み込まれたになり、呼び出す関数のドライバーの*AddDevice*ルーチン。 関数のドライバーでは、FDO を作成し、デバイス スタックを結び付けます。

-   省略可能な上位レベルのフィルター ドライバーは、各デバイスのフィルター操作を作成します。

    PnP マネージャーにより、関数のドライバーと呼び出しの後に読み込まれるすべての省略可能な上位レベルのフィルター ドライバーは、デバイスに対して存在する場合、 *AddDevice*ルーチン。 各フィルター ドライバーでは、デバイス スタックをそのデバイス オブジェクトをアタッチします。

要約すると、デバイス スタックには、特定のデバイスの I/O の処理に関係する各ドライバーのデバイス オブジェクトが含まれています。 親のバス ドライバーは、PDO、関数のドライバーが FDO、および各オプションのフィルター ドライバーが、フィルター操作を行います。

すべてのデバイス、bus adapter/コント ローラー デバイスおよび nonbus デバイスがあること、PDO と FDO デバイス スタックに注意してください。 バス アダプタ/コント ローラーの PDO は、親のバスのバス ドライバーによって作成されます。 たとえば、SCSI アダプターは、PCI バスに接続されるため、PCI バス ドライバーは、SCSI アダプターの PDO を作成します。

Raw モードで、デバイスは使用されている場合、関数またはフィルター ドライバー (FDO またはフィルター DOs) はありません。 親のバス ドライバーと 0 個以上のバス フィルター DOs PDO だけがあります。

参照してください[デバイス オブジェクトを作成する](creating-a-device-object.md)についてドライバー ルーチンは作成して、デバイス オブジェクトのアタッチを担当します。

デバイス スタックといくつか追加の情報を構成、 *devnode*デバイス。 PnP マネージャーが存在する場合は、デバイスが起動されているかどうかや、どのドライバーなど、デバイスの devnode の情報を保持、デバイス上の変更の通知を登録します。 カーネル デバッガー コマンド **! devnode** devnode についての情報が表示されます。

 

 




