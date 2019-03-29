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
ms.openlocfilehash: 116843f42de7234ae8c4d1cd23fe0b5a8c3b8ed9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581578"
---
# <a name="handling-unsupported-srbfunctionxxx"></a>処理のサポートされていない SRB\_関数\_XXX


## <span id="ddk_handling_unsupported_srb_function_xxx_kg"></span><span id="DDK_HANDLING_UNSUPPORTED_SRB_FUNCTION_XXX_KG"></span>


すべて*HwScsiStartIo*ルーチンは、サポートされていない SRB の確認メッセージを処理する必要があります\_関数\_*XXX*次のようにします。

1.  セットの入力 SRB の**SrbStatus** SRB に\_状態\_無効な\_を要求します。

2.  呼び出す[ **ScsiPortNotification** ](https://msdn.microsoft.com/library/windows/hardware/ff564657)で、 *NotificationType * * * RequestComplete** SRB の入力を使用しています。

3.  呼び出す**ScsiPortNotification**を使用して、* NotificationType ***NextRequest**、または**NextLuRequest** HBA は、タグが付けられたキューをサポートしているかあたり複数の要求論理ユニット。

4.  コントロールを返します。

 

 




