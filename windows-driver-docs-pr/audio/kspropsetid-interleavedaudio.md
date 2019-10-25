---
title: KSPROPSETID\_InterleavedAudio
description: KSK PROPSETID\_InterleavedAudio プロパティセットは、オーディオデバイスドライバーによって実装されます。このドライバーは、ループバックオーディオとキャプチャオーディオのインターリーブに関する追加情報を提供します。
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7c2c5d8aed23f5233c94e2a5d5e58051425d15e4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832674"
---
# <a name="kspropsetid_interleavedaudio"></a>KSPROPSETID\_InterleavedAudio

**Ksk Propsetid\_InterleavedAudio**プロパティセットは、オーディオデバイスドライバーによって実装されます。これには、オーディオストリームのループバックオーディオとキャプチャオーディオのインターリーブに関する追加情報が含まれます。

**Kspropsetid\_InterleavedAudio**は、windows 10 バージョン19H1 以降のバージョンの windows で使用できます。

*Ksmedia .h*ヘッダーファイルでは、次のように**ksk Propsetid\_InterleavedAudio**プロパティセットが定義されています。

``` syntax
#define STATIC_KSPROPSETID_InterleavedAudio\
    0xe9ebe550, 0xd619, 0x4c0a, 0x97, 0x6b, 0x70, 0x62, 0x32, 0x2b, 0x30, 0x6
DEFINE_GUIDSTRUCT("E9EBE550-D619-4C0A-976B-7062322B3006", KSPROPSETID_InterleavedAudio);
#define KSPROPSETID_InterleavedAudio DEFINE_GUIDNAMED(KSPROPSETID_InterleavedAudio)
```

**Kspropsetid\_InterleavedAudio**プロパティセットには、次の KS プロパティが含まれています。

[**KSK プロパティ\_INTERLEAVEDAUDIO_FORMATINFORMATION**](ksproperty-interleavedaudio-formatinformation.md)

このプロパティ名は、 [**Ksk プロパティ\_INTERLEAVEDAUDIO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ne-ksmedia-ksproperty_interleavedaudio) enum で定義されています。
