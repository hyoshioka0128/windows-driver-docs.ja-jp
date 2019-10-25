---
title: NFP デバイス識別子
description: NFP デバイス識別子
ms.assetid: B387D3F8-A9A7-47F0-B5E3-8437581947E4
keywords:
- NFC
- 近距離無線通信
- proximity
- 近距離近接通信
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41543e6ac407fb9fc607729272b4d605582422da
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843426"
---
# <a name="nfp-device-identifiers"></a>NFP デバイス識別子


NFP デバイスドライバーのデバイス識別子は次のとおりです。

-   デバイスインターフェイスクラス
    -   GUID\_DEVINTERFACE\_NFP
    -   "{FB3842CD-9E2A-4F83-8FCC-4B0761139AE9}"
-   デバイスクラス GUID
    -   "{5630831C09 7-F5D32586E060}" のようになります。
-   Device Class
    -   近く
    -   これは、Windows 8 以降の OS で定義されたデバイスクラスです。 このインターフェイスを公開するドライバーは、このデバイスクラスと一致する必要があります。
-   DEVPKEY\_NFP\_機能
    -   0Xfb3842 Cd、0x9E2A、0x4F83、0x8F、0xCC、0x4B、0x07、0x61、0x13、0x9A、0xE9、0x02

デバイスが NFC として提供されている場合、ドライバーは、公開された GUID\_DEVINTERFACE\_NFP\_インターフェイスに対して DEVPKEY\_NFP\_機能を設定する必要があります。entry: "StandardNfc"。

 

 
## <a name="related-topics"></a>関連トピック
[NFC デバイスドライバーインターフェイス (DDI) の概要](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  
[近距離無線近接 DDI リファレンス](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)  

