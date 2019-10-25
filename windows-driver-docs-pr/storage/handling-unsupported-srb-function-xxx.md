---
title: サポートされていない SRB_FUNCTION_XXX の処理
description: サポートされていない SRB_FUNCTION_XXX の処理
ms.assetid: 95b9288c-290f-4908-9de3-11d68ed624e2
keywords:
- SCSI ミニポートドライバー WDK 記憶域、HwScsiStartIo
- HwScsiStartIo
- サポートされていない SRB_FUNCTION_XXX
- サポートされていない SRB_FUNCTION_XXX
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0cae8f7c6c8ebf5f7aec914f0c6d3561c6a46eec
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833713"
---
# <a name="handling-unsupported-srb_function_xxx"></a>サポートされていない SRB\_関数の処理\_XXX


## <span id="ddk_handling_unsupported_srb_function_xxx_kg"></span><span id="DDK_HANDLING_UNSUPPORTED_SRB_FUNCTION_XXX_KG"></span>


各*HwScsiStartIo*ルーチンは、次のように、サポートされていない SRB\_関数\_*XXX*の受信を処理する必要があります。

1.  入力 SRB の**Srbstatus**を SRB\_STATUS\_無効な\_要求に設定します。

2.  *NotificationType * * * RequestComplete** と入力 SRB を使用して[**ScsiPortNotification**](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/nf-srb-scsiportnotification)を呼び出します。

3.  **ScsiPortNotification**をもう一度呼び出すには、* NotificationType ***nextrequest**を使用するか、HBA がタグ付きキューをサポートしている場合は**nextlurequest**を、論理ユニットあたりは複数の要求をサポートします。

4.  制御を返します。

 

 




