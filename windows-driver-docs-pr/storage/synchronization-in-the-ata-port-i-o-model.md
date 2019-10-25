---
title: ATA ポート I/O モデルでの同期
description: ATA ポート I/O モデルでの同期
ms.assetid: 91b95588-8cf7-4833-84c2-a991fd066fb2
keywords:
- ATA ポートドライバー WDK、同期
- 同期 WDK ATA ポートドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e46f0f6eea97d3a0a2814ab9f0d31f101243ea2a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844453"
---
# <a name="synchronization-in-the-ata-port-io-model"></a>ATA ポート I/O モデルでの同期


## <span id="ddk_synchronization_in_the_ata_port_i_o_model_kg"></span><span id="DDK_SYNCHRONIZATION_IN_THE_ATA_PORT_I_O_MODEL_KG"></span>


**メモ**ATA ポートドライバーと ATA ミニポートドライバーのモデルは、将来変更されるか、使用できなくなる可能性があります。 代わりに、 [storport ドライバー](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver)および[storport ミニポート](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)ドライバーモデルを使用することをお勧めします。


Ata ポートドライバーは、ATA ミニポートドライバールーチンによって、デバイス拡張機能などの重要なデータ構造へのアクセスを同期するように構成できます。 割り込みハンドラーによるアクセスは、他のミニポートドライバールーチンによるアクセスと同期されることが特に重要です。これらのアクセスは、異なるスレッドコンテキスト内で発生する可能性があるためです。

ATA ポートドライバーは、2つの同期モードのどちらかで動作します。 1つのモードでは、ミニポートドライバーは割り込みサービスルーチンと同期されます。 それ以外のモードでは同期されません。 ATA ミニポートドライバーは、 [**IDE\_チャネル\_構成**](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/ns-irb-_ide_channel_configuration)構造の**syncwithisr**メンバーを設定することによって、同期モードを指定できます。 ミニポートドライバーによって**Syncwithisr**が**TRUE**に設定されている場合、ATA ポートドライバーは、 [**IdeHwInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/nc-irb-ide_hw_initialize)、 [**IdeHwStartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/nc-irb-ide_hw_startio)、または[**IdeHwReset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/nc-irb-ide_hw_reset)のいずれかのミニポートドライバールーチンを呼び出す前に、dirql に IRQL を発生させます。 次の表は、 **Syncwithisr**に割り当てられた値が、ata ポートドライバーが ata ミニポートドライバールーチンを呼び出す IRQL にどのように影響するかを示しています。

**チャネルインターフェイスのミニポートドライバールーチン**

**IRQL**

**SyncWithIsr = TRUE**

**SyncWithIsr = FALSE**

***AtaChannelInitRoutine***

パッシブ\_レベル

パッシブ\_レベル

***IdeHwControl***

(パラメーターの ControlAction = StartChannel)

パッシブ\_レベル

パッシブ\_レベル

***IdeHwControl***

(パラメーターの ControlAction = StopChannel)

パッシブ\_レベル

パッシブ\_レベル

***IdeHwControl***

(パラメーターの ControlAction = PowerUpChannel)

&lt;= ディスパッチ\_レベル

&lt;= ディスパッチ\_レベル

***IdeHwControl***

(パラメーターの ControlAction = PowerDownChannel)

&lt;= ディスパッチ\_レベル

&lt;= ディスパッチ\_レベル

***IdeHwBuildIo***

&lt;= ディスパッチ\_レベル

&lt;= ディスパッチ\_レベル

ワーカールーチン (コールバック)

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

同期ルーチン ( [**AtaPortRequestSynchronizedRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/nf-irb-ataportrequestsynchronizedroutine)によって指定されたコールバックルーチン)

DIRQL

DIRQL

***IdeHwInterrupt***

DIRQL

DIRQL

 

**Syncwithisr**が**FALSE**に設定されている場合でも、ミニポートドライバーは、 [**AtaPortRequestSynchronizedRoutine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/nf-irb-ataportrequestsynchronizedroutine)を呼び出してコールバックルーチンへのポインターを渡すことによって、コールバックルーチンを割り込みハンドラーと同期できます。

同期はチャネル単位で行われます。 このため、同期されたチャネルでは、2つのミニポートドライバールーチンが同時に実行されることはありませんが、同期された別のチャネルで実行されるルーチンは同時に実行できます。

 

 


