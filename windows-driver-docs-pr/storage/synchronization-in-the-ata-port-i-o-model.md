---
title: ATA ポート I/O モデルでの同期
description: ATA ポート I/O モデルでの同期
ms.assetid: 91b95588-8cf7-4833-84c2-a991fd066fb2
keywords:
- ATA ポート ドライバー WDK、同期
- WDK ATA ポート ドライバーの同期
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e655a9b912a92c6eababb37151f63e926092d0c2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349139"
---
# <a name="synchronization-in-the-ata-port-io-model"></a>ATA ポート I/O モデルでの同期


## <span id="ddk_synchronization_in_the_ata_port_i_o_model_kg"></span><span id="DDK_SYNCHRONIZATION_IN_THE_ATA_PORT_I_O_MODEL_KG"></span>


**注**ATA ポートはドライバーと ATA ミニポート ドライバー モデルが変更されるか利用今後します。 代わりに、使用をお勧め、 [Storport ドライバー](https://msdn.microsoft.com/windows/hardware/drivers/storage/storport-driver)と[Storport ミニポート](https://msdn.microsoft.com/windows/hardware/drivers/storage/storport-miniport-drivers)ドライバー モデル。


ATA のミニポート ドライバーのルーチンで、デバイスの拡張機能などの重要なデータ構造へのアクセスを同期する ATA ポート ドライバーを構成できます。 別のスレッドのコンテキスト内でこれらのアクセスが発生する可能性があるため他のミニポート ドライバー ルーチンによってアクセスと、割り込みハンドラーによるアクセスが同期されているが特に重要です。

ATA ポート ドライバーは、2 つの同期モードのいずれかで動作できます。 1 つのモードでは、ミニポート ドライバーが割り込みサービス ルーチンと同期されます。 その他のモードでこれは同期されません。 ATA のミニポート ドライバーは、同期モードを設定して指定できます、 **SyncWithIsr**のメンバー、 [ **IDE\_チャネル\_構成**](https://msdn.microsoft.com/library/windows/hardware/ff559029)構造体。 ミニポート ドライバーが設定されている場合**SyncWithIsr**に**TRUE**の次のミニポート ドライバー ルーチンを呼び出す前に、ATA ポート ドライバーが DIRQL に IRQL を発生させます。[**IdeHwInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff557467)、 [ **IdeHwStartIo**](https://msdn.microsoft.com/library/windows/hardware/ff559003)、または[ **IdeHwReset**](https://msdn.microsoft.com/library/windows/hardware/ff558998)します。 次の表に値を割り当てる方法を示します**SyncWithIsr** IRQL を ATA ポート ドライバー ルーチンを呼び出して ATA ミニポート ドライバーに影響を与えます。

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

同期ルーチン (で指定されたコールバック ルーチン[ **AtaPortRequestSynchronizedRoutine**](https://msdn.microsoft.com/library/windows/hardware/ff550223))

DIRQL

DIRQL

***IdeHwInterrupt***

DIRQL

DIRQL

 

場合でも**SyncWithIsr**に設定されている**FALSE**、ミニポート ドライバーは、割り込みハンドラーとコールバック ルーチンを呼び出すことで同期できる[ **AtaPortRequestSynchronizedRoutine** ](https://msdn.microsoft.com/library/windows/hardware/ff550223)コールバック ルーチンへのポインターを渡します。

同期は、チャネルごとのです。 そのため、同期のチャンネルを同時に 2 つのミニポート ドライバーのルーチンは実行されませんが、別の同期されたチャネルで実行されているルーチンを同時に実行できます。

 

 


