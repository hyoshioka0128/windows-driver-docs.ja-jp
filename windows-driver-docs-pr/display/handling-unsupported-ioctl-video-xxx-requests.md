---
title: サポートされていない IOCTL_VIDEO_XXX 要求の処理
description: サポートされていない IOCTL_VIDEO_XXX 要求の処理
ms.assetid: e3a96cc2-bb7f-4060-bf71-d8a63b918329
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000、要求の処理
- 要求処理の WDK ビデオのミニポート
- サポートされていない IOCTL_VIDEO_XXX 要求 WDK ビデオ ミニポート
- IOCTL_VIDEO_XXX 要求 WDK のビデオのミニポート
- I/O WDK ビデオのミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9fcd563a2b3529fb78ecfd7d70e18602769b7cc4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353909"
---
# <a name="handling-unsupported-ioctlvideoxxx-requests"></a>処理のサポートされていない IOCTL\_ビデオ\_XXX 要求


## <span id="ddk_handling_unsupported_ioctl_video_xxx_requests_gg"></span><span id="DDK_HANDLING_UNSUPPORTED_IOCTL_VIDEO_XXX_REQUESTS_GG"></span>


すべて[ *HwVidStartIO* ](https://msdn.microsoft.com/library/windows/hardware/ff567367)関数もサポートされていない IOCTL の確認メッセージを処理する必要があります\_ビデオ\_*XXX*、次のようにします。

1.  セットの入力 VRP の**状態**エラー フィールド\_無効な\_関数。

2.  セットの入力 VRP の**情報**フィールドをゼロにします。

3.  返す**TRUE**を要求の処理を示します。

参照してください、 [**ビデオ\_要求\_パケット**](https://msdn.microsoft.com/library/windows/hardware/ff570547)と[**状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff569732)の構造体詳細についてはします。

 

 





