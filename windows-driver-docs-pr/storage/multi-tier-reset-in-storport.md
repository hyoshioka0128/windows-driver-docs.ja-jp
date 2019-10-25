---
title: Storport の多階層リセット
description: Storport の多階層リセット
ms.assetid: 11c717b9-5154-43dd-b357-ff093cabec4b
keywords:
- Storport ドライバー WDK、エラー
- エラー WDK Storport
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67b919419424826368d3f79293a2a8ee56a8cabf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845091"
---
# <a name="multi-tier-reset-in-storport"></a>Storport の多階層リセット


## <span id="ddk_multi_tier_reset_in_storport_kg"></span><span id="DDK_MULTI_TIER_RESET_IN_STORPORT_KG"></span>


Storport ドライバーは、SCSI ポートドライバーよりも高度なリセットスキームを実装しています。 Scsi バス上でも、バス全体をリセットする SCSI ポートの手法は負荷の高い操作です。 高パフォーマンスのバス (ファイバーチャネルバスなど) では、バスのリセットが不可能な場合もあります。

可能な場合は、Storport ドライバーおよび関連する上位レベルのドライバーが論理ユニットをリセットしようとします。 これが失敗した場合、Storport はデバイスのリセットを試みます。 最後に、この方法も失敗した場合、Storport によってバスがリセットされます。 このシーケンスでは、バスリセット操作が大幅に減少します。

高パフォーマンスバスのより複雑な要件に対処するために、Storport では、さまざまなリセットオプションを可能にする多層リセット操作を実装しています。 SRBs を介して送信されるリセットには、1つではなく、要求できる2種類があります。

最後に、バスのリセット操作は、同期コールバックルーチン[**HwStorResetBus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/storport/nc-storport-hw_reset_bus)によって行われます。

 

 




