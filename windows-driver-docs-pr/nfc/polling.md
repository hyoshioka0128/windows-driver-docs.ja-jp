---
title: NFC のポーリング
description: NFC のポーリング
ms.assetid: C6C531EC-59AA-4AF5-903E-A726C0E79E47
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d099d6b189ef9cdc618df03eab1fdf48da3798ac
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569933"
---
# <a name="nfc-polling"></a>NFC のポーリング


(NFC) などの多くの NFP テクノロジは、近接デバイスとタグの存在を検出するためにポーリングする必要があります。 必要に応じて、ポーリングする必要があります電力効率の高い方法で行う必要があります頻繁とき NFP テクノロジは、ユーザーへの応答が表示されます。

### <a name="required-actions"></a>必要な操作

NFP テクノロジをポーリングする必要がある場合、は、近接デバイスまたはタグが検出された場合を除き、PC の Cpu のいずれかのスリープを解除せずハードウェアでポーリングが実行する必要があります。 また、ポーリング レートは、1 秒間 (500 ミリ秒ごと) に 2 回以上でなければなりません。 推奨されるポーリング間隔では、1 秒あたり 4 ~ 5 倍です。

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
 

