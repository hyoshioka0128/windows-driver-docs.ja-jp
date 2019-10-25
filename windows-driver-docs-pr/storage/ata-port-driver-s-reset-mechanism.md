---
title: ATA ポート ドライバーのリセット メカニズム
description: ATA ポート ドライバーのリセット メカニズム
ms.assetid: adc27819-d1ae-4b97-8109-5d742c0595d3
keywords:
- ATA ポートドライバー WDK、リセットメカニズム
- メカニズムのリセット WDK ATA ポートドライバー
- LUN が WDK ATA ポートドライバーをリセットする
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37df2d3374bb4600a8504427c0bcb3ed14ec2c28
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845098"
---
# <a name="ata-port-drivers-reset-mechanism"></a>ATA ポート ドライバーのリセット メカニズム


## <span id="ddk_ata_port_drivers_reset_mechanism_kg"></span><span id="DDK_ATA_PORT_DRIVERS_RESET_MECHANISM_KG"></span>

**メモ**ATA ポートドライバーと ATA ミニポートドライバーのモデルは、将来変更されるか、使用できなくなる可能性があります。 代わりに、 [storport ドライバー](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver)および[storport ミニポート](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)ドライバーモデルを使用することをお勧めします。



ATA ポートドライバーは、Storport ドライバーのリセットメカニズムと同様の点で、2層リセットメカニズムをサポートしています。 Storport リセットメカニズムの詳細については、「 [storport での多層リセット](multi-tier-reset-in-storport.md)」を参照してください。

SCSI ポートドライバーとは異なり、Storport ドライバーと同様に、ATA ポートドライバーは、可能な限りバス全体をリセットすることを回避します。 ATA ポートドライバーは、最初に個々の LUN をリセットしようとします。これは、関数の値が IRB\_関数\_LUN\_リセットされます。 リセットが失敗した場合、ATA ポートドライバーはバス全体をリセットします。

たとえば、LUN の未完了の要求の1つがタイムアウトした後に、ATA ポートドライバーが LUN をリセットする IRB を発行するとします。この LUN のリセットに応答して、ミニポートドライバーはデバイスのリセット操作を実行します。ハードウェアがこの操作をサポートしている場合は、リセット IRB を含めて、LUN 上のすべての未処理の要求を完了します。 リセット IRB は、タイムアウトしません。 そのため、ミニポートドライバーがリセット IRB を完了しないと、追加の要求は LUN に発行されません。

ミニポートドライバーがリセット IRB に失敗した場合 (つまり、IRB\_STATUS\_SUCCESS) 以外の状態のリセット IRB を完了した場合、ATA ポートドライバーはミニポートドライバーの[**IdeHwReset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/nc-irb-ide_hw_reset)ルーチンを呼び出して、チャネル全体をリセットします。 その後、ミニポートドライバーは、そのチャネルに対する未処理の要求をすべて完了し、ハードウェアに対して必要な操作を実行して、そのチャネルに接続されているデバイスをリセットする必要があります。

ATA ポートドライバーでは、複数の Lun を持つデバイスのターゲットリセットはサポートされていません。

 

 


