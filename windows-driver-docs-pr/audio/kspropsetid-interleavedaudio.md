---
title: KSPROPSETID\_InterleavedAudio
description: KSPROPSETID\_InterleavedAudio プロパティ セットは、オーディオをキャプチャしてループバック オーディオの割り込みについて追加情報を提供するオーディオ デバイス ドライバによって実装されます。
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 19699f56b023b94917203f51a7b3eb1279acef60
ms.sourcegitcommit: 71938460f3d04caa4b4d6d0cee695db887ee35e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58136107"
---
# <a name="kspropsetidinterleavedaudio"></a>KSPROPSETID\_InterleavedAudio

**KSPROPSETID\_InterleavedAudio**プロパティ セットは、ループバック オーディオの割り込みに関する追加情報を含み、オーディオ ストリーム内のオーディオをキャプチャするオーディオ デバイス ドライバによって実装されます。

**KSPROPSETID\_InterleavedAudio**は Windows 10 バージョン 19 H 1 およびそれ以降のバージョンの Windows で使用できます。

*Ksmedia.h*ヘッダー ファイルの定義、 **KSPROPSETID\_InterleavedAudio**プロパティを次のように設定します。

``` syntax
#define STATIC_KSPROPSETID_InterleavedAudio\
    0xe9ebe550, 0xd619, 0x4c0a, 0x97, 0x6b, 0x70, 0x62, 0x32, 0x2b, 0x30, 0x6
DEFINE_GUIDSTRUCT("E9EBE550-D619-4C0A-976B-7062322B3006", KSPROPSETID_InterleavedAudio);
#define KSPROPSETID_InterleavedAudio DEFINE_GUIDNAMED(KSPROPSETID_InterleavedAudio)
```

**KSPROPSETID\_InterleavedAudio**プロパティ セットには、次の KS プロパティが含まれています。

[**KSPROPERTY\_INTERLEAVEDAUDIO_FORMATINFORMATION**](ksproperty-interleavedaudio-formatinformation.md)

このプロパティ名が定義されている、 [ **KSPROPERTY\_INTERLEAVEDAUDIO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ne-ksmedia-ksproperty_interleavedaudio)列挙型。
