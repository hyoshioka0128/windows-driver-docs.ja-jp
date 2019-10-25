---
title: NFP の無効化
description: クライアントは、サブスクリプション、パブリケーション、およびプレゼンスを一時的に無効にすることができます。
ms.assetid: 94BE6D24-60AD-45BD-AF2D-388022114975
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1c8f5850637cd8fc78f1735e67795a3c56aa0f2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843424"
---
# <a name="disabling-nfp"></a>NFP の無効化


クライアントは、サブスクリプション、パブリケーション、およびプレゼンスを一時的に無効にすることができます。

サブスクリプション、パブリケーション、およびプレゼンスを一時的に無効にするには、 [**IOCTL\_NFP\_DISABLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/nfpdev/ni-nfpdev-ioctl_nfp_disable)をハンドルに送信します。 これは、クライアントが近接機能を無効にする必要があり、リソースを割り当てられたままにしておく必要がある場合に便利です。

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[近距離無線近接 DDI リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

