---
title: Storport の多階層リセット
description: Storport の多階層リセット
ms.assetid: 11c717b9-5154-43dd-b357-ff093cabec4b
keywords:
- Storport ドライバー WDK、エラー
- WDK Storport のエラー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 865a3e4e6c96ead2631fc55fe0218fe84466e62b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384661"
---
# <a name="multi-tier-reset-in-storport"></a>Storport の多階層リセット


## <span id="ddk_multi_tier_reset_in_storport_kg"></span><span id="DDK_MULTI_TIER_RESET_IN_STORPORT_KG"></span>


Storport ドライバーでは、SCSI ポートのドライバーよりもより高度なリセット パターンを実装します。 全体のバスのリセットの SCSI ポート手法は、SCSI バス上であっても、負荷の高い操作です。 ファイバー チャネル バスなどの高パフォーマンスのバスのバスのリセットもできない可能性があります。

可能であれば、Storport ドライバーと関連する高度なドライバーは、論理ユニットのリセットを試みる。 これが失敗すると、Storport、デバイスをリセットしようとします。 最後に、このアプローチも失敗した場合、Storport、バスをリセットします。 このシーケンスは、バスのリセット操作の数が少ないを生成します。

高パフォーマンスのバスのより複雑な要件に対処するには、Storport より多様なオプションのリセットを許可する多階層のリセット操作を実装します。 1 つではなく、要求できるされる Srb 経由で送信されるリセットの 2 種類あります。

バスのリセット操作に影響があります、同期コールバック ルーチンを最後に、 [ **HwStorResetBus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/storport/nc-storport-hw_reset_bus)します。

 

 




