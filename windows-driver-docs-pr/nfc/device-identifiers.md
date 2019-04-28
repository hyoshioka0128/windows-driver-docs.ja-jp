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
ms.openlocfilehash: 35c5832c12c7748297d1215d79f1fef8d7323dff
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375222"
---
# <a name="nfp-device-identifiers"></a>NFP デバイス識別子


次に、NFP デバイス ドライバーに対するデバイスの id。

-   デバイスのインターフェイス クラス
    -   GUID\_DEVINTERFACE\_NFP
    -   "{FB3842CD-9E2A-4F83-8FCC-4B0761139AE9}"
-   デバイス クラス GUID
    -   "{5630831C-06C9-4856-B327-F5D32586E060}"
-   Device Class
    -   「近く」
    -   これは、Windows 8 以降では、OS で定義されたデバイス クラスです。 このインターフェイスを公開するドライバーは、このデバイスのクラスと一致する必要があります。
-   DEVPKEY\_NFP\_機能
    -   0xFB3842CD、0x9E2A、0x4F83、0x8F、0 xcc、0x4B、0x07、0x61、0x13、0x9A、0xE9、0x02

NFC として、デバイスが提供されると、ドライバーは DEVPKEY を入力する必要があります\_NFP\_で公開されている GUID の機能を\_DEVINTERFACE\_NFP インターフェイス、DEVPROP\_型\_文字列\_1 つのエントリを含むリストのプロパティ。"StandardNfc"。

 

 
## <a name="related-topics"></a>関連トピック
[NFC のデバイス ドライバー インターフェイス (DDI) の概要](https://msdn.microsoft.com/library/windows/hardware/mt715815)  
[フィールドの近接 DDI 参照の近く](https://msdn.microsoft.com/library/windows/hardware/jj866056)  

