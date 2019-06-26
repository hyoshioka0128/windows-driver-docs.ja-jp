---
title: 形式タグとサブ形式 GUID の間の変換
description: 形式タグとサブ形式 GUID の間の変換
ms.assetid: 299ad5d3-df62-41cf-a18f-daa83cc60ef3
keywords:
- 非 PCM オーディオ形式 WDK、サブフォーマット GUID 変換
- Guid の WDK オーディオを subformat します。
- 形式のタグとサブフォーマット Guid に変換します。
- 交差部分のデータ ハンドラーの WDK オーディオ、wave 形式の非 PCM
- Guid の WDK オーディオ
- wave 形式のタグの WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 490bcf5702cf0dfadd51af6e15b47770e5883458
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355583"
---
# <a name="converting-between-format-tags-and-subformat-guids"></a>形式タグとサブ形式 GUID の間の変換


## <span id="converting_between_format_tags_and_subformat_guids"></span><span id="CONVERTING_BETWEEN_FORMAT_TAGS_AND_SUBFORMAT_GUIDS"></span>


PCM 以外の波を処理するためのガイドライン\_形式\_拡張可能な形式は、wave 形式のタグで指定されている PCM 以外の形式に似ています。 具体的には、WAVE\_形式\_拡張可能な形式は、PCM の形式の場合、ファクトリから別の暗証番号 (pin) ファクトリが必要で、独自のデータ範囲の交差部分ハンドラーを必要とします。

Wave オーディオ形式\_形式\_の GUID で拡張可能な形式が指定された、**サブフォーマット**のメンバー、 [ **KSDATAFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksdataformat)構造体。 Wave 形式の登録済みのすべてのタグが対応するサブフォーマット定義によって生成される GUID、\_WAVEFORMATEX\_Ksmedia.h で GUID マクロ。 WAVE に対応する GUID など\_形式\_DOLBY\_AC3\_SPDIF タグが定義として定義されている\_WAVEFORMATEX\_GUID (WAVE\_形式\_DOLBY\_AC3\_SPDIF)。

Ksmedia.h から次のコード スニペットでは、autoinitialized 静的変数として新しい GUID を定義する方法を示します。

```cpp
#define STATIC_KSDATAFORMAT_SUBTYPE_WAVEFORMATEX \
 0x00000000L, 0x0000, 0x0010, 0x80, 0x00, 0x00, 0xaa, 0x00, 0x38, 0x9b, 0x71
DEFINE_GUIDSTRUCT("00000000-0000-0010-8000-00aa00389b71", KSDATAFORMAT_SUBTYPE_WAVEFORMATEX);
#define KSDATAFORMAT_SUBTYPE_WAVEFORMATEX DEFINE_GUIDNAMED(KSDATAFORMAT_SUBTYPE_WAVEFORMATEX)
```

Ksmedia.h からこれらのマクロは、wave 形式のタグとその関連付けられている Guid の間で変換します。

```cpp
#if !defined( DEFINE_WAVEFORMATEX_GUID )
#define DEFINE_WAVEFORMATEX_GUID(x) \
    (USHORT)(x), 0x0000, 0x0010, 0x80, 0x00, 0x00, 0xaa, 0x00, 0x38, 0x9b, 0x71
#endif

#define INIT_WAVEFORMATEX_GUID(Guid, x) \
{ \
    *(Guid) = KSDATAFORMAT_SUBTYPE_WAVEFORMATEX; \
    (Guid)->Data1 = (USHORT)(x); \
}

#define IS_VALID_WAVEFORMATEX_GUID(Guid) \
    (!memcmp(((PUSHORT)&KSDATAFORMAT_SUBTYPE_WAVEFORMATEX) + 1, \
    ((PUSHORT)(Guid)) + 1, sizeof(GUID) - sizeof(USHORT)))

#define EXTRACT_WAVEFORMATEX_ID(Guid)(USHORT)((Guid)->Data1)
```

次のサンプル コードはサブフォーマット WAVE wave 形式のタグに基づいている GUID を作成するには、この手法を組み合わせて\_形式\_AC3\_SPDIF、0x0092 値。

```cpp
#define STATIC_KSDATAFORMAT_SUBTYPE_DOLBY_AC3_SPDIF \
    DEFINE_WAVEFORMATEX_GUID(WAVE_FORMAT_DOLBY_AC3_SPDIF)

DEFINE_GUIDSTRUCT("00000092-0000-0010-8000-00aa00389b71",
    KSDATAFORMAT_SUBTYPE_DOLBY_AC3_SPDIF);

#define KSDATAFORMAT_SUBTYPE_DOLBY_AC3_SPDIF \
    DEFINE_GUIDNAMED(KSDATAFORMAT_SUBTYPE_DOLBY_AC3_SPDIF)
...
INIT_WAVEFORMATEX_GUID(pMyGuid,myWaveFormatTag);
...
if (IS_VALID_WAVEFORMATEX_GUID(aWaveFormatExGuidPtr)) {
    aWaveFormatTag = EXTRACT_WAVEFORMATEX_ID(aWaveFormatExGuidPtr);
}
```

 

 




