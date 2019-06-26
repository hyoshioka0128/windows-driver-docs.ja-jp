---
title: KSPROPSETID\_AudioModule
description: KSPROPSETID\_AudioModule プロパティ セットは、オーディオのモジュールの一覧を取得する、オーディオ ドライバーによって使用されています。
ms.assetid: 6F167E5E-CA11-45F3-BF21-6B9A3F90DB9F
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c0b7568a52d88a8d49a99e84a7722b567eae2fb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360494"
---
# <a name="kspropsetidaudiomodule"></a>KSPROPSETID\_AudioModule


**KSPROPSETID\_AudioModule**オーディオ ドライバー、オーディオのモジュールの一覧を取得するプロパティ セットが使用されます。

*Ksmedia.h*ヘッダー ファイルの定義、 **KSPROPSETID\_AudioModule**プロパティを次のように設定します。

``` syntax
#define STATIC_KSPROPSETID_AudioModule \
    0xc034fdb0, 0xff75, 0x47c8, 0xaa, 0x3c, 0xee, 0x46, 0x71, 0x6b, 0x50, 0xc6
DEFINE_GUIDSTRUCT("C034FDB0-FF75-47C8-AA3C-EE46716B50C6", KSPROPSETID_AudioModule);
#define KSPROPSETID_AudioModule DEFINE_GUIDNAMED(KSPROPSETID_AudioModule)
```

**KSPROPSETID\_AudioModule**プロパティ セットには、次の KS プロパティが含まれています。

[**KSPROPERTY\_AUDIOMODULE\_記述子**](ksproperty-audiomodule-descriptors.md)

[**KSPROPERTY\_AUDIOMODULE\_コマンド**](ksproperty-audiomodule-command.md)

[**KSPROPERTY\_AUDIOMODULE\_通知\_デバイス\_ID**](ksproperty-audiomodule-notification-device-id.md)

このプロパティ名が定義されている、 [ **KSPROPERTY\_AUDIOMODULE** ](ksproperty-audiomodule.md)列挙型。

オーディオのモジュールの詳細については、次を参照してください。[オーディオ モジュールの検出を実装する](https://docs.microsoft.com/windows-hardware/drivers/audio/implementing-audio-module-communication)します。

 

 





