---
title: Storport の多階層のリセット
description: Storport の多階層のリセット
ms.assetid: 11c717b9-5154-43dd-b357-ff093cabec4b
keywords:
- Storport ドライバー WDK、エラー
- WDK Storport のエラー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0313a9e2c2982f752cc1dc5b576bd7af2757843d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532510"
---
# <a name="multi-tier-reset-in-storport"></a>Storport の多階層のリセット


## <span id="ddk_multi_tier_reset_in_storport_kg"></span><span id="DDK_MULTI_TIER_RESET_IN_STORPORT_KG"></span>


Storport ドライバーでは、SCSI ポートのドライバーよりもより高度なリセット パターンを実装します。 全体のバスのリセットの SCSI ポート手法は、SCSI バス上であっても、負荷の高い操作です。 ファイバー チャネル バスなどの高パフォーマンスのバスのバスのリセットもできない可能性があります。

可能であれば、Storport ドライバーと関連する高度なドライバーは、論理ユニットのリセットを試みる。 これが失敗すると、Storport、デバイスをリセットしようとします。 最後に、このアプローチも失敗した場合、Storport、バスをリセットします。 このシーケンスは、バスのリセット操作の数が少ないを生成します。

高パフォーマンスのバスのより複雑な要件に対処するには、Storport より多様なオプションのリセットを許可する多階層のリセット操作を実装します。 1 つではなく、要求できるされる Srb 経由で送信されるリセットの 2 種類あります。

バスのリセット操作に影響があります、同期コールバック ルーチンを最後に、 [ **HwStorResetBus**](https://msdn.microsoft.com/library/windows/hardware/ff557415)します。

 

 




