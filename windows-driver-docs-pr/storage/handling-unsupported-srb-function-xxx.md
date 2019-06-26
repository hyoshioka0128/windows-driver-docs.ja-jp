---
title: サポートされていない SRB_FUNCTION_XXX の処理
description: サポートされていない SRB_FUNCTION_XXX の処理
ms.assetid: 95b9288c-290f-4908-9de3-11d68ed624e2
keywords:
- SCSI ミニポート ドライバー WDK ストレージ、HwScsiStartIo
- HwScsiStartIo
- サポートされていない SRB_FUNCTION_XXX
- サポートされていない SRB_FUNCTION_XXX
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53764b5a0dea1f3800db006f6a58d29dbbe44dfe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371156"
---
# <a name="handling-unsupported-srbfunctionxxx"></a>処理のサポートされていない SRB\_関数\_XXX


## <span id="ddk_handling_unsupported_srb_function_xxx_kg"></span><span id="DDK_HANDLING_UNSUPPORTED_SRB_FUNCTION_XXX_KG"></span>


すべて*HwScsiStartIo*ルーチンは、サポートされていない SRB の確認メッセージを処理する必要があります\_関数\_*XXX*次のようにします。

1.  セットの入力 SRB の**SrbStatus** SRB に\_状態\_無効な\_を要求します。

2.  呼び出す[ **ScsiPortNotification** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportnotification)で、 *NotificationType * * * RequestComplete** SRB の入力を使用しています。

3.  呼び出す**ScsiPortNotification**を使用して、* NotificationType ***NextRequest**、または**NextLuRequest** HBA は、タグが付けられたキューをサポートしているかあたり複数の要求論理ユニット。

4.  コントロールを返します。

 

 




