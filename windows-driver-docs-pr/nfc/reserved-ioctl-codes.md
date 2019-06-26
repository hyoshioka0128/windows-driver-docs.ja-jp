---
title: 予約済みの IOCTL コード
ms.assetid: A2A67F8E-0A29-429E-935C-39368EFD9772
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
description: コードについては予約済みの ioctl NFC ドライバーは、STATUS_INVALID_DEVICE_STATE を返す必要があります。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 226a61dd529991313a5415e7397111d75c0466b1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386511"
---
# <a name="reserved-ioctl-codes"></a>予約済みの IOCTL コード


次のすべての IOCTL コードが予約されています。 上述明示的に定義されていない場合ドライバーは、状態を返す必要があります\_無効な\_デバイス\_から、次のいずれかの状態。

CTL\_コード (ファイル\_デバイス\_NFP、0x0000、 \*、 \*) を通じて CTL\_コード (ファイル\_デバイス\_NFP、0x00FF、 \*、 \*)

次の Ioctl は IHV 固有の機能を使用できます。

CTL\_コード (ファイル\_デバイス\_NFP、0x0100、 \*、 \*) を通じて CTL\_コード (ファイル\_デバイス\_NFP、0x01FF、 \*、 \*)

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
[フィールドの近接 DDI 参照の近く](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)  
