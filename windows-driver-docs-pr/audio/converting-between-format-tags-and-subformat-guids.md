---
title: 形式タグとサブ形式 GUID の間の変換
description: 形式タグとサブ形式 GUID の間の変換
ms.assetid: 299ad5d3-df62-41cf-a18f-daa83cc60ef3
keywords:
- PCM 以外のオーディオ形式 WDK、subformat GUID 変換
- subformat Guid WDK オーディオ
- 書式設定タグとサブ形式 Guid の変換
- データ交差ハンドラー WDK オーディオ、PCM 以外の wave 形式
- Guid WDK オーディオ
- WDK オーディオの wave 形式タグ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b75f60c7fa13485279c47fbe2f9d53dcc6d1c14d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833587"
---
# <a name="converting-between-format-tags-and-subformat-guids"></a>形式タグとサブ形式 GUID の間の変換


## <span id="converting_between_format_tags_and_subformat_guids"></span><span id="CONVERTING_BETWEEN_FORMAT_TAGS_AND_SUBFORMAT_GUIDS"></span>


PCM 以外の WAVE\_フォーマット\_拡張可能な形式を処理するためのガイドラインは、wave 形式のタグで指定される PCM 以外の形式の場合と似ています。 具体的には、WAVE\_形式\_拡張可能な形式では、PCM 形式のファクトリとは別にピンファクトリが必要であり、独自のデータ範囲の交差ハンドラーが必要です。

WAVE\_形式\_拡張可能形式のオーディオ形式は、 [**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)構造体の**SUBFORMAT**メンバーの GUID によって指定されます。 すべての登録済みの wave 形式タグには、対応するサブフォーマット GUID があります。これは、WAVEFORMATEX の DEFINE\_\_GUID マクロによって生成されます。 たとえば、WAVE\_形式\_DOLBY\_AC3\_SPDIF タグに対応する GUID は、DEFINE\_WAVEFORMATEX\_GUID (WAVE\_形式\_DOLBY\_AC3\_SPDIF) として定義されています。

Ksk からのこのコードスニペットは、新しい GUID を自動初期化された静的変数として定義する方法を示しています。

```cpp
#define STATIC_KSDATAFORMAT_SUBTYPE_WAVEFORMATEX \
 0x00000000L, 0x0000, 0x0010, 0x80, 0x00, 0x00, 0xaa, 0x00, 0x38, 0x9b, 0x71
DEFINE_GUIDSTRUCT("00000000-0000-0010-8000-00aa00389b71", KSDATAFORMAT_SUBTYPE_WAVEFORMATEX);
#define KSDATAFORMAT_SUBTYPE_WAVEFORMATEX DEFINE_GUIDNAMED(KSDATAFORMAT_SUBTYPE_WAVEFORMATEX)
```

次のような Ksk からのマクロは、wave 形式のタグとそれに関連付けられている Guid を変換します。

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

次のサンプルコードでは、これらの手法を組み合わせて、波形形式のタグ WAVE\_形式\_AC3\_SPDIF に基づくサブフォーマット GUID を作成しています。これは、値0x0092 です。

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

 

 




