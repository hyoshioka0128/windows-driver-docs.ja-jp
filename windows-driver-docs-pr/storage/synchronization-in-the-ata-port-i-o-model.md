---
title: ATA ポート I/O モデルでの同期
description: ATA ポート I/O モデルでの同期
ms.assetid: 91b95588-8cf7-4833-84c2-a991fd066fb2
keywords:
- ATA ポート ドライバー WDK、同期
- WDK ATA ポート ドライバーの同期
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91d62a16f94d32fec7c25a1d2ba239ded2e38a54
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368167"
---
# <a name="synchronization-in-the-ata-port-io-model"></a>ATA ポート I/O モデルでの同期


## <span id="ddk_synchronization_in_the_ata_port_i_o_model_kg"></span><span id="DDK_SYNCHRONIZATION_IN_THE_ATA_PORT_I_O_MODEL_KG"></span>


**注**ATA ポートはドライバーと ATA ミニポート ドライバー モデルが変更されるか利用今後します。 代わりに、使用をお勧め、 [Storport ドライバー](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver)と[Storport ミニポート](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)ドライバー モデル。


ATA のミニポート ドライバーのルーチンで、デバイスの拡張機能などの重要なデータ構造へのアクセスを同期する ATA ポート ドライバーを構成できます。 別のスレッドのコンテキスト内でこれらのアクセスが発生する可能性があるため他のミニポート ドライバー ルーチンによってアクセスと、割り込みハンドラーによるアクセスが同期されているが特に重要です。

ATA ポート ドライバーは、2 つの同期モードのいずれかで動作できます。 1 つのモードでは、ミニポート ドライバーが割り込みサービス ルーチンと同期されます。 その他のモードでこれは同期されません。 ATA のミニポート ドライバーは、同期モードを設定して指定できます、 **SyncWithIsr**のメンバー、 [ **IDE\_チャネル\_構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/ns-irb-_ide_channel_configuration)構造体。 ミニポート ドライバーが設定されている場合**SyncWithIsr**に**TRUE**の次のミニポート ドライバー ルーチンを呼び出す前に、ATA ポート ドライバーが DIRQL に IRQL を発生させます。[**IdeHwInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/nc-irb-ide_hw_initialize)、 [ **IdeHwStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/nc-irb-ide_hw_startio)、または[ **IdeHwReset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/nc-irb-ide_hw_reset)します。 次の表に値を割り当てる方法を示します**SyncWithIsr** IRQL を ATA ポート ドライバー ルーチンを呼び出して ATA ミニポート ドライバーに影響を与えます。

**チャネル インターフェイスのミニポート ドライバー ルーチン**

**IRQL**

**SyncWithIsr = TRUE**

**SyncWithIsr = FALSE**

***AtaChannelInitRoutine***

パッシブ\_レベル

パッシブ\_レベル

***IdeHwControl***

(パラメーター ControlAction StartChannel =)

パッシブ\_レベル

パッシブ\_レベル

***IdeHwControl***

(パラメーター ControlAction StopChannel =)

パッシブ\_レベル

パッシブ\_レベル

***IdeHwControl***

(パラメーター ControlAction PowerUpChannel =)

&lt;= ディスパッチ\_レベル

&lt;= ディスパッチ\_レベル

***IdeHwControl***

(パラメーター ControlAction PowerDownChannel =)

&lt;= ディスパッチ\_レベル

&lt;= ディスパッチ\_レベル

***IdeHwBuildIo***

&lt;= ディスパッチ\_レベル

&lt;= ディスパッチ\_レベル

ワーカー ルーチン (コールバック)

ディスパッチ\_レベル

ディスパッチ\_レベル

***IdeHwInitialize***

DIRQL

ディスパッチ\_レベル

***IdeHwStartIo***

DIRQL

ディスパッチ\_レベル

***IdeHwReset***

DIRQL

ディスパッチ\_レベル

同期ルーチン (で指定されたコールバック ルーチン[ **AtaPortRequestSynchronizedRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/nf-irb-ataportrequestsynchronizedroutine))

DIRQL

DIRQL

***IdeHwInterrupt***

DIRQL

DIRQL

 

場合でも**SyncWithIsr**に設定されている**FALSE**、ミニポート ドライバーは、割り込みハンドラーとコールバック ルーチンを呼び出すことで同期できる[ **AtaPortRequestSynchronizedRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/nf-irb-ataportrequestsynchronizedroutine)コールバック ルーチンへのポインターを渡します。

同期は、チャネルごとのです。 そのため、同期のチャンネルを同時に 2 つのミニポート ドライバーのルーチンは実行されませんが、別の同期されたチャネルで実行されているルーチンを同時に実行できます。

 

 


