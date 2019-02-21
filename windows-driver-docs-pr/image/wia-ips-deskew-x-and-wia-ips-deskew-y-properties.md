---
title: WIA_IPS_DESKEW_X と WIA_IPS_DESKEW_Y プロパティ
description: WIA_IPS_DESKEW_X と WIA_IPS_DESKEW_Y プロパティ
ms.assetid: 748b08f7-e838-4df8-abcb-4ff1cdd20f7e
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e9ff1f68ba577b524912289ab1ed02b81da3e02
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56550000"
---
# <a name="wiaipsdeskewx-and-wiaipsdeskewy-properties"></a>WIA\_IP\_DESKEW\_X と WIA\_IP\_DESKEW\_Y プロパティ





[ **WIA\_IP\_DESKEW\_X** ](https://msdn.microsoft.com/library/windows/hardware/ff552581)と[ **WIA\_IP\_DESKEW\_Y** ](https://msdn.microsoft.com/library/windows/hardware/ff552587)デスキュー ドライバーがサポートしている場合、プロパティは、スキャナー ドライバーによって実装されます。 これら 2 つのプロパティの説明、傾斜したイメージの 2 つの上端がによって定義された外接する四角形内にある[ **WIA\_IP\_XPOS**](https://msdn.microsoft.com/library/windows/hardware/ff552663)、 [**WIA\_IP\_YPOS**](https://msdn.microsoft.com/library/windows/hardware/ff552671)、 [ **WIA\_IP\_XEXTENT**](https://msdn.microsoft.com/library/windows/hardware/ff552661)、および[**WIA\_IP\_YEXTENT** ](https://msdn.microsoft.com/library/windows/hardware/ff552669)プロパティ。

WIA の有効な値\_IP\_DESKEW\_X が 0 の間である必要があり、(WIA\_IP\_XEXTENT − 1)。 WIA の有効な値\_IP\_DESKEW\_Y が 0 の間である必要があり、(WIA\_IP\_YEXTENT − 1)。 両方のプロパティに対して 0 の値は、スキューの修正を実行しないことを意味します。

これら 2 つの値が一意にする deskewed するイメージの位置を定義するため、スキャンの長方形の領域のみがサポートされます。 Deskew 角度は、これら 2 つの値から計算できます。

 

 




