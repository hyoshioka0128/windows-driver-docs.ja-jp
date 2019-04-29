---
title: KSPROPSETID\_AudioEngine
description: KSPROPSETID\_AudioEngine プロパティ セットに、オーディオ ドライバーを使用して、ハードウェアのオーディオ エンジン ノードの詳細情報 KS プロパティが含まれています。
ms.assetid: F3155DF6-0710-4941-94DC-478A8F5DE8D1
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3eaf256d66414c9b410c0afff49867c50cbb221f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332546"
---
# <a name="kspropsetidaudioengine"></a>KSPROPSETID\_AudioEngine


**KSPROPSETID\_AudioEngine**プロパティ セットに、オーディオ ドライバーを使用して、ハードウェアのオーディオ エンジン ノードの詳細情報 KS プロパティが含まれています。

**KSPROPSETID\_AudioEngine**は Windows 8 および Windows オペレーティング システムの以降のバージョンで使用できます。

ハードウェア ソリューションでは、オーディオ オフロードをサポートするときに、ハードウェアのオーディオ ドライバーは、Windows 8 ユーザー モードのオーディオ スタックはこれらの機能を検出し、それを活用できるように特定の方法でその機能を公開する必要があります。

Windows 8 で提供されるオーディオのオフロード アーキテクチャをサポートするには、ハードウェア ソリューションは、ハードウェアのオーディオ エンジンを実装する必要があります。 このハードウェアのオーディオ ドライバーは、KS フィルター内に含まれる (KS) ノードをストリーミングするオーディオ エンジン カーネルとしてハードウェア オーディオ エンジンを公開する必要があります。 この目的は新しく定義されているノード型[ **KSNODETYPE\_オーディオ\_エンジン**](ksnodetype-audio-engine.md)します。 [ **KSPROPERTY\_AUDIOENGINE** ](ksproperty-audioengine.md)新しい KS プロパティを表す列挙を使用します。

*Ksmedia.h*ヘッダー ファイルの定義、 **KSPROPSETID\_AudioEngine**プロパティを次のように設定します。

``` syntax
#define STATIC_KSPROPSETID_AudioEngine\
    0x3A2F82DCL, 0x886F, 0x4BAA, 0x9E, 0xB4, 0x8, 0x2B, 0x90, 0x25, 0xC5, 0x36
DEFINE_GUIDSTRUCT("3A2F82DC-886F-4BAA-9EB4-082B9025C536", KSPROPSETID_AudioEngine);
#define KSPROPSETID_AudioEngine DEFINE_GUIDNAMED(KSPROPSETID_AudioEngine)
```

**KSPROPSETID\_AudioEngine**プロパティ セットには、次の KS プロパティが含まれています。

## <span id="wdk_kspropsetid_audioengine"></span><span id="WDK_KSPROPSETID_AUDIOENGINE"></span>


[**KSPROPERTY\_AUDIOENGINE\_バッファー\_サイズ\_範囲**](ksproperty-audioengine-buffer-size-limits.md)

[**KSPROPERTY\_AUDIOENGINE\_記述子**](ksproperty-audioengine-descriptor.md)

[**KSPROPERTY\_AUDIOENGINE\_DEVICEFORMAT**](ksproperty-audioengine-deviceformat.md)

[**KSPROPERTY\_AUDIOENGINE\_GFXENABLE**](ksproperty-audioengine-gfx-enable.md)

[**KSPROPERTY\_AUDIOENGINE\_LFXENABLE**](ksproperty-audioengine-lfx-enable.md)

[**KSPROPERTY\_AUDIOENGINE\_ループバック\_保護**](ksproperty-audioengine-loopback-protection.md)

[**KSPROPERTY\_AUDIOENGINE\_MIXFORMAT**](ksproperty-audioengine-mixformat.md)

[**KSPROPERTY\_AUDIOENGINE\_SUPPORTEDDEVICEFORMATS**](ksproperty-audioengine-supporteddeviceformats.md)

[**KSPROPERTY\_AUDIOENGINE\_VOLUMELEVEL**](ksproperty-audioengine-volumelevel.md)

これらのプロパティ名が定義されている、 [ **KSPROPERTY\_AUDIOENGINE** ](ksproperty-audioengine.md)列挙型。

 

 





