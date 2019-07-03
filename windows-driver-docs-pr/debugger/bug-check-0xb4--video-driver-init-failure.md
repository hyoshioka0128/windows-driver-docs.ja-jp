---
title: バグ チェックの繰り返し、0xB4 VIDEO_DRIVER_INIT_FAILURE
description: VIDEO_DRIVER_INIT_FAILURE のバグ チェックでは、0x000000B4 の値を持ちます。 これは、Windows がグラフィックス モードに切り替わるできなかったことを示します。
ms.assetid: 37c2d07d-f351-42d0-ba88-9b9a2a3d19f8
keywords:
- バグ チェックの繰り返し、0xB4 VIDEO_DRIVER_INIT_FAILURE
- VIDEO_DRIVER_INIT_FAILURE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- VIDEO_DRIVER_INIT_FAILURE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 20ea652b025a52b4049c0a64bdafb1a728cbc9d1
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519012"
---
# <a name="bug-check-0xb4-videodriverinitfailure"></a>バグ チェック 0xB4:ビデオ\_ドライバー\_INIT\_エラー


ビデオ\_ドライバー\_INIT\_エラーのバグ チェックが 0x000000B4 の値を持ちます。 これは、Windows がグラフィックス モードに切り替わるできなかったことを示します。

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターを使用しているときに、エラー コードがブルー スクリーンが受信した顧客の場合を参照してください。[トラブルシューティング ブルー スクリーン エラー](https://www.windows.com/stopcode)します。


## <a name="videodriverinitfailure-parameters"></a>ビデオ\_ドライバー\_INIT\_エラー パラメーター


なし

<a name="cause"></a>原因
-----

システムは、ディスプレイ ドライバーを開始することがないため、グラフィックス モードに移動できませんでした。

これは通常、ビデオのミニポート ドライバーを正常に読み込むことがない場合に発生します。

 

 




