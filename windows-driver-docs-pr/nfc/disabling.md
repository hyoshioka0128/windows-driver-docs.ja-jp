---
title: NFP を無効にします。
description: クライアントは、サブスクリプション、パブリケーション、およびプレゼンスに一時的に無効にできます。
ms.assetid: 94BE6D24-60AD-45BD-AF2D-388022114975
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38c4d2f1538c0564ea64fc373dcca6ec572ddd3a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370538"
---
# <a name="disabling-nfp"></a>NFP を無効にします。


クライアントは、サブスクリプション、パブリケーション、およびプレゼンスに一時的に無効にできます。

サブスクリプション、パブリケーション、およびプレゼンスを一時的に無効には送信することによって行われます[ **IOCTL\_NFP\_を無効にする**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/nfpdev/ni-nfpdev-ioctl_nfp_disable)ハンドルにします。 これは、機能は、クライアントが近接通信機能を無効にするには迅速に再度有効にするために必要なときに割り当てられたリソースを保持する場合に便利です。

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[フィールドの近接 DDI 参照の近く](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  

