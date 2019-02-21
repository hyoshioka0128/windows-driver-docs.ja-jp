---
title: ATA のポートの I/O モデル スキャッター/ギャザー リストへのアクセス
description: ATA のポートの I/O モデル スキャッター/ギャザー リストへのアクセス
ms.assetid: 56221602-9588-47f2-acd9-a11bd5ce02d9
keywords:
- ATA ポート ドライバー WDK、スキャッター/ギャザー一覧
- スキャッター/ギャザー WDK ATA ポート ドライバーの一覧
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6531a47bdfd9654114d47cf578b37a99464d2d7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56529152"
---
# <a name="access-to-scattergather-lists-in-the-ata-port-io-model"></a>ATA のポートの I/O モデル スキャッター/ギャザー リストへのアクセス


## <span id="ddk_access_to_scatter_gather_lists_in_the_ata_port_i_o_model_kg"></span><span id="DDK_ACCESS_TO_SCATTER_GATHER_LISTS_IN_THE_ATA_PORT_I_O_MODEL_KG"></span>

**注**ATA ポートはドライバーと ATA ミニポート ドライバー モデルが変更されるか利用今後します。 代わりに、使用をお勧め、 [Storport ドライバー](https://msdn.microsoft.com/windows/hardware/drivers/storage/storport-driver)と[Storport ミニポート](https://msdn.microsoft.com/windows/hardware/drivers/storage/storport-miniport-drivers)ドライバー モデル。



[ATA ポート I/O モデル](ata-port-i-o-model.md)など、 [Storport I/O モデル](storport-i-o-model.md)システムのスキャッター/ギャザー リスト構造に直接アクセスするミニポート ドライバーを提供します。 この直接アクセスでは、ミニポート ドライバーは、そのプライベート スキャッター/ギャザーの一覧を作成するポートのドライバー サポート ルーチンに加える必要がある呼び出しの数を減らします。

SCSI ポートの I/O モデルがミニポート ドライバーを手動で検出し、繰り返しの呼び出しを通じて、独自のスキャッター/ギャザー リストをビルドを強制する一方で、 [ **ScsiPortGetPhysicalAddress** ](https://msdn.microsoft.com/library/windows/hardware/ff564636)ルーチン。

使用して、システムのスキャッター/ギャザーの一覧に直接アクセスできる ATA ポート ミニポート ドライバー、 [ **AtaPortGetScatterGatherList** ](https://msdn.microsoft.com/library/windows/hardware/ff550164)ルーチン。 スキャッター/ギャザーを一覧表示する**AtaPortGetScatterGatherList** IRB が完了するまでのみが有効な値を取得します。

ミニポート ドライバーがスキャッター/ギャザーを一覧表示するには、メモリを解放する必要はありません**AtaPortGetScatterGatherList**を返します。

ミニポート ドライバーの[ **IdeHwBuildIo** ](https://msdn.microsoft.com/library/windows/hardware/ff557462)必要がある場合、ルーチンは、スキャッター/ギャザー リストを変換する必要があります。

 

 


