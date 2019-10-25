---
title: NFC ポーリング
description: NFC ポーリング
ms.assetid: C6C531EC-59AA-4AF5-903E-A726C0E79E47
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e55e6b870c11aebce6e71af9de488fc5436e759a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831510"
---
# <a name="nfc-polling"></a>NFC ポーリング


近接のデバイスとタグの存在を検出するには、多くの NFP テクノロジ (NFC など) がポーリングされる必要があります。 必要に応じて、電源効率の高い方法でポーリングを行う必要があります。また、NFP テクノロジがユーザーに応答していると思われるほど多くの場合にポーリングを行う必要があります。

### <a name="required-actions"></a>必要なアクション

NFP テクノロジがポーリングを行う必要がある場合、近接デバイスまたはタグが検出されない限り、コンピューターの Cpu をスリープ解除せずに、ハードウェアでポーリングを行う必要があります。 また、ポーリング速度は、1秒あたり少なくとも2回 (500 ミリ秒ごと) にする必要があります。 推奨されるポーリング速度は、1秒あたり4-5 回です。

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
 

