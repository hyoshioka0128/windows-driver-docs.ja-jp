---
title: ATA ポート I/O モデル
description: ATA ポート I/O モデル
ms.assetid: 6feaf2c4-63b2-4ab2-9d4d-7259406be652
keywords:
- ATA ポート ドライバー WDK、I/O
- I/O WDK ATA ポート ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 402b4a219759dd92d834ce0fdb2debab27dc9e7c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368400"
---
# <a name="ata-port-io-model"></a>ATA ポート I/O モデル


## <span id="ddk_ata_port_i_o_model_kg"></span><span id="DDK_ATA_PORT_I_O_MODEL_KG"></span>

**注**ATA ポートはドライバーと ATA ミニポート ドライバー モデルが変更されるか利用今後します。 代わりに、使用をお勧め、 [Storport ドライバー](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver)と[Storport ミニポート](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)ドライバー モデル。



ATA ポート ドライバー、Storport ドライバーと同様には、I/O のプッシュ モデルを使用します。 これは、ドライバーが入力を要求するミニポート ドライバーを待つことがなく、重複するパケットの最大数までのミニポート ドライバーに非同期 I/O 要求を転送することを意味します。 プッシュ モデルでは、ポート、ドライバーは、I/O 要求のフローを制御し、ミニポート ドライバーに要求をプッシュします。

その一方で、SCSI ポート ドライバーは、I/O のプル モデルを使用します。 I/O のプル モデルでは、SCSI ポート ドライバーは、ミニポート ドライバーへの I/O 要求を同期的に転送し、[次へ] の I/O 要求を送信する前に、新しい入力を要求するミニポート ドライバーに待機します。 さらに、ミニポート ドライバーでは、I/O 要求のフローを制御し、ポート ドライバーからの要求をプルダウンします。

Storport ドライバーの I/O モデルの詳細については、次を参照してください。 [Storport I/O モデル](storport-i-o-model.md)します。

SCSI ポート ドライバーの I/O モデルの詳細については、次を参照してください。 [SCSI ポート I/O モデル](scsi-port-i-o-model.md)します。

 

 


