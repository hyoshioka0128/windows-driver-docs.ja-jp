---
title: KSPROPSETID\_AudioSignalProcessing
description: KSPROPSETID\_AudioSignalProcessing プロパティ セットは、pin factory でサポートされるオーディオ信号処理モードの一覧を取得する、オーディオ ドライバーによって使用されています。
ms.assetid: D9EF0D65-4DCD-4936-B7AC-A17FA50D3AE7
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1acdb33d84430f41eccc4114f33b1421d3df4b3c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549643"
---
# <a name="kspropsetidaudiosignalprocessing"></a>KSPROPSETID\_AudioSignalProcessing


**KSPROPSETID\_AudioSignalProcessing** pin factory でサポートされるオーディオ信号処理モードの一覧を取得するプロパティ セットがオーディオ ドライバーによって使用されます。

*Ksmedia.h*ヘッダー ファイルの定義、 **KSPROPSETID\_AudioSignalProcessing**プロパティを次のように設定します。

``` syntax
#define STATIC_KSPROPSETID_AudioEffectsDiscovery\  
    0xb217a72, 0x16b8, 0x4a4d, 0xbd, 0xed, 0xf9, 0xd6, 0xbb, 0xed, 0xcd, 0x8f  
DEFINE_GUIDSTRUCT("0B217A72-16B8-4A4D-BDED-F9D6BBEDCD8F", KSPROPSETID_AudioEffectsDiscovery);  
#define KSPROPSETID_AudioEffectsDiscovery DEFINE_GUIDNAMED(KSPROPSETID_AudioEffectsDiscovery)
```

**KSPROPSETID\_AudioSignalProcessing**プロパティ セットには、次の KS プロパティが含まれています。

[**KSPROPERTY\_AUDIOSIGNALPROCESSING\_モード**](ksproperty-audiosignalprocessing-modes.md)

このプロパティ名が定義されている、 [ **KSPROPERTY\_AUDIOSIGNALPROCESSING** ](ksproperty-audiosignalprocessing.md)列挙型。

 

 





