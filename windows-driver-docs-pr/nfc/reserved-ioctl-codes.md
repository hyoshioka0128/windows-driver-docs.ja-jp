---
title: 予約済みの IOCTL コード
ms.assetid: A2A67F8E-0A29-429E-935C-39368EFD9772
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
description: NFC ドライバーの予約済み ioctl コードに関する情報。 STATUS_INVALID_DEVICE_STATE を返す必要があります。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c57e740f24ffc479e5388398145dc6da4f28d800
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834025"
---
# <a name="reserved-ioctl-codes"></a>予約済みの IOCTL コード


上記のすべての IOCTL コードは、明示的に定義されている場合を除いて予約されています。ドライバーは、次のいずれかの状態\_無効\_デバイス\_状態を返す必要があります。

Ctl \*コード (ファイル\_デバイス\_NFP、0x00FF、\_、\*) を使用して、ctl\_コード (ファイル\_デバイス\_NFP、0x0000、\*、\*)

次の Ioctl は、IHV 固有の機能に使用できます。

Ctl\_コード (ファイル\_デバイス\_NFP、0x0100、\*、\*) から CTL\_コード (ファイル\_デバイス\_NFP、0x01FF、\*、\*)

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[近距離無線近接 DDI リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
