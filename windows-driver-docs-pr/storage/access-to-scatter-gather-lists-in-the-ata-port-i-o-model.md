---
title: ATA ポート I/O モデルでのスキャッター/ギャザー リストへのアクセス
description: ATA ポート I/O モデルでのスキャッター/ギャザー リストへのアクセス
ms.assetid: 56221602-9588-47f2-acd9-a11bd5ce02d9
keywords:
- ATA ポートドライバー WDK、スキャッター/ギャザーリスト
- スキャッター/ギャザーリスト WDK ATA ポートドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be39e32b5330735f90c0546530a19c64c6253ce8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839618"
---
# <a name="access-to-scattergather-lists-in-the-ata-port-io-model"></a>ATA ポート I/O モデルでのスキャッター/ギャザー リストへのアクセス


## <span id="ddk_access_to_scatter_gather_lists_in_the_ata_port_i_o_model_kg"></span><span id="DDK_ACCESS_TO_SCATTER_GATHER_LISTS_IN_THE_ATA_PORT_I_O_MODEL_KG"></span>

**メモ**ATA ポートドライバーと ATA ミニポートドライバーのモデルは、将来変更されるか、使用できなくなる可能性があります。 代わりに、 [storport ドライバー](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver)および[storport ミニポート](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)ドライバーモデルを使用することをお勧めします。



[Storport I/o モデル](storport-i-o-model.md)などの[ATA ポート i/o モデル](ata-port-i-o-model.md)には、システムのスキャッター/ギャザーリスト構造に直接アクセスできるミニポートドライバーが用意されています。 この直接アクセスにより、ミニポートドライバーがプライベートのスキャッター/ギャザーリストを構築するためにポートドライバーサポートルーチンに対して行う必要がある呼び出しの回数が減ります。

一方、SCSI ポート i/o モデルでは、 [**ScsiPortGetPhysicalAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportgetphysicaladdress)ルーチンを繰り返し呼び出すことで、ミニポートドライバーが手動で検出し、独自のスキャッター/gather リストを構築するようにします。

ATA ポートミニポートドライバーは、 [**AtaPortGetScatterGatherList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/nf-irb-ataportgetscattergatherlist)ルーチンを使用して、システムのスキャッター/ギャザー一覧に直接アクセスできます。 **AtaPortGetScatterGatherList**が返すスキャッター/ギャザーリストは、IRB が完了するまで有効です。

ミニポートドライバーは、 **AtaPortGetScatterGatherList**から返されるスキャッター/ギャザーリストのメモリを解放する必要はありません。

必要に応じて、ミニポートドライバーの[**IdeHwBuildIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/irb/nc-irb-ide_hw_buildio)ルーチンは、スキャッター/ギャザーリストを変換する必要があります。

 

 


