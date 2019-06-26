---
title: ATA ポート ドライバーのリセット メカニズム
description: ATA ポート ドライバーのリセット メカニズム
ms.assetid: adc27819-d1ae-4b97-8109-5d742c0595d3
keywords:
- ATA ポート ドライバー WDK、メカニズムをリセットします。
- WDK ATA ポート ドライバーのメカニズムをリセットします。
- LUN は、WDK ATA ポート ドライバーをリセットします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e589f8b1b3cc51f60c515f3e612192797575fbe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368397"
---
# <a name="ata-port-drivers-reset-mechanism"></a>ATA ポート ドライバーのリセット メカニズム


## <span id="ddk_ata_port_drivers_reset_mechanism_kg"></span><span id="DDK_ATA_PORT_DRIVERS_RESET_MECHANISM_KG"></span>

**注**ATA ポートはドライバーと ATA ミニポート ドライバー モデルが変更されるか利用今後します。 代わりに、使用をお勧め、 [Storport ドライバー](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver)と[Storport ミニポート](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)ドライバー モデル。



ATA のポート ドライバーでは、いくつかの点で、Storport ドライバーのリセットのメカニズムのような 2 階層のリセットのメカニズムをサポートします。 詳細については、Storport のリセットのメカニズムを参照してください。 [Storport の多層をリセット](multi-tier-reset-in-storport.md)します。

Storport ドライバーと SCSI ポート ドライバーとは異なり、ATA ポート ドライバーは、可能な限り全体のバスのリセットを回避します。 ATA ポート ドライバーが最初に、IRB を IRB の関数値を使用して個々 の LUN をリセットしようと\_関数\_LUN\_をリセットします。 リセットに失敗した場合、ATA ポート ドライバーは、全体のバスをリセットします。

たとえば、ATA ポート ドライバーの問題を IRB LUN の未完了の要求の 1 つがタイムアウトした後に、LUN をリセットするとします。この LUN のリセットに応答してでは、ミニポート ドライバーは、ハードウェアがサポートしているとリセット IRB を含む LUN 上のすべての未処理要求が完了する場合に、デバイスのリセット操作を実行します。 リセット IRB はありませんがタイムアウトしました。 そのため追加の要求は発行されません、LUN に、ミニポート ドライバーが IRB リセットが完了しない場合。

ミニポート ドライバー IRB リセットに失敗した場合 (つまり、IRB IRB 以外のすべての状態のリセットが完了した\_状態\_成功)、ATA ポート ドライバー呼び出し、ミニポート ドライバーの[ **IdeHwReset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/irb/nc-irb-ide_hw_reset)ルーチン全体のチャネルをリセットします。 ミニポート ドライバーはそのチャネルの未処理のすべての要求を完了する必要がありますし、そのチャネルに関連付けられているデバイスをリセットするハードウェア上で必要な操作を実行します。

ATA ポート ドライバーは、複数の Lun がデバイスのターゲットのリセットをサポートしていません。

 

 


