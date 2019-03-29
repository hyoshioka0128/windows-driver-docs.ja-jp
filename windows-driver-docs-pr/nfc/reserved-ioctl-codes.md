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
ms.openlocfilehash: b8c17429afe64a4c7171363ebd757767182645f4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574601"
---
# <a name="reserved-ioctl-codes"></a>予約済みの IOCTL コード


次のすべての IOCTL コードが予約されています。 上述明示的に定義されていない場合ドライバーは、状態を返す必要があります\_無効な\_デバイス\_から、次のいずれかの状態。

CTL\_コード (ファイル\_デバイス\_NFP、0x0000、 \*、 \*) を通じて CTL\_コード (ファイル\_デバイス\_NFP、0x00FF、 \*、 \*)

次の Ioctl は IHV 固有の機能を使用できます。

CTL\_コード (ファイル\_デバイス\_NFP、0x0100、 \*、 \*) を通じて CTL\_コード (ファイル\_デバイス\_NFP、0x01FF、 \*、 \*)

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[フィールドの近接 DDI 参照の近く](https://msdn.microsoft.com/library/windows/hardware/jj866056)  
