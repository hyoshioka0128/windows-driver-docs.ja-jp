---
title: KSPROPSETID\_AudioEffectsDiscovery
description: KSPROPSETID\_AudioEffectsDiscovery プロパティ セットは、マイクロソフトの汎用プロキシ オーディオ処理オブジェクト (APO) を使用するオーディオ デバイス ドライバによって実装されます。
ms.assetid: 68229885-1446-4BF0-B4E1-96A777006567
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b1c2797c662fae927f8215feba171fa642f5ae1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571350"
---
# <a name="kspropsetidaudioeffectsdiscovery"></a>KSPROPSETID\_AudioEffectsDiscovery


**KSPROPSETID\_AudioEffectsDiscovery**プロパティ セットは、マイクロソフトの汎用プロキシ オーディオ処理オブジェクト (APO) を使用するオーディオ デバイス ドライバによって実装されます。

**KSPROPSETID\_AudioEffectsDiscovery**は Windows 8.1 と Windows オペレーティング システムの以降のバージョンで使用できます。

*MsApoFxProxy.h*ヘッダー ファイルの定義、 **KSPROPSETID\_AudioEffectsDiscovery**プロパティを次のように設定します。

``` syntax
#define STATIC_KSPROPSETID_AudioEffectsDiscovery\  
    0xb217a72, 0x16b8, 0x4a4d, 0xbd, 0xed, 0xf9, 0xd6, 0xbb, 0xed, 0xcd, 0x8f  
DEFINE_GUIDSTRUCT("0B217A72-16B8-4A4D-BDED-F9D6BBEDCD8F", KSPROPSETID_AudioEffectsDiscovery);  
#define KSPROPSETID_AudioEffectsDiscovery DEFINE_GUIDNAMED(KSPROPSETID_AudioEffectsDiscovery)
```

**KSPROPSETID\_AudioEffectsDiscovery**プロパティ セットには、次の KS プロパティが含まれています。

[**KSPROPERTY\_AUDIOEFFECTSDISCOVERY\_EFFECTSLIST**](https://msdn.microsoft.com/library/windows/hardware/dn457706)

このプロパティ名が定義されている、 [ **KSPROPERTY\_AUDIOEFFECTSDISCOVERY** ](https://msdn.microsoft.com/library/windows/hardware/dn457705)列挙型。

 

 





