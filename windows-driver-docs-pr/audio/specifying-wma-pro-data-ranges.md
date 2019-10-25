---
title: WMA Pro データ範囲の指定
description: WMA Pro データ範囲の指定
ms.assetid: c7e9bc68-cec2-4a34-9ef0-ce3c9a4cc987
keywords:
- S/PDIF パススルー WDK オーディオ
- WMA Pro over S/PDIF 形式 WDK オーディオ
- 非 PCM 形式のオーディオ (WDK)
- PCM 以外のオーディオ形式 WDK、S/PDIF
- WMA Pro WDK オーディオ
- Sony/お持ちのデジタルインターフェイス
- データ範囲 WDK オーディオ、WMA Pro
- PCM 以外のオーディオ形式 WDK、WMA Pro
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31cd9656009bee911ab154bd03ee96f12bbdb1ac
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832409"
---
# <a name="specifying-wma-pro-data-ranges"></a>WMA Pro データ範囲の指定


## <span id="specifying_wma_pro_data_ranges"></span><span id="SPECIFYING_WMA_PRO_DATA_RANGES"></span>


ヘッダーファイル Mmreg では、値0x0164 が定義されています。これは、WMA Pro の wave 形式タグになります (S/PDIF)。

```cpp
  #define WAVE_FORMAT_WMASPDIF  0x0164
```

対応する形式とサブタイプの GUID は、次\_のように、ヘッダーファイルの WAVEFORMATEX\_GUID マクロを使用して、wave 形式のタグの観点から指定できます。

```cpp
  #define KSDATAFORMAT_SUBTYPE_WMA_SPDIF    \
                      DEFINE_WAVEFORMATEX_GUID(WAVE_FORMAT_WMASPDIF)
```

次のコード例では、WaveCyclic または WavePci ミニポートドライバーが、WMA Pro over S/PDIF 形式および AC-3 over-S/PDIF 形式をサポートしているピンに対して、 [**Ksk datarの\_オーディオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)テーブルエントリを指定する方法を示します。

```cpp
static KSDATARANGE_AUDIO PinDataRangesSpdifOut[] =
{
  // 48-kHz WMA Pro over S/PDIF
  {
    {
      sizeof(KSDATARANGE_AUDIO),
      0,
      0,
      0,
      STATICGUIDOF(KSDATAFORMAT_TYPE_AUDIO),
      STATICGUIDOF(KSDATAFORMAT_SUBTYPE_WMA_SPDIF),
      STATICGUIDOF(KSDATAFORMAT_SPECIFIER_WAVEFORMATEX)
    },
    2,       // Max number of channels
    16,      // Minimum number of bits per sample
    16,      // Maximum number of bits per channel
    48000,   // Minimum rate
    48000    // Maximum rate
  },

  // 44.1-kHz WMA Pro over S/PDIF
  {
    {
      sizeof(KSDATARANGE_AUDIO),
      0,
      0,
      0,
      STATICGUIDOF(KSDATAFORMAT_TYPE_AUDIO),
      STATICGUIDOF(KSDATAFORMAT_SUBTYPE_WMA_SPDIF),
      STATICGUIDOF(KSDATAFORMAT_SPECIFIER_WAVEFORMATEX)
    },
    2,       // Max number of channels
    16,      // Minimum number of bits per sample
    16,      // Maximum number of bits per channel
    44100,   // Minimum rate
    44100    // Maximum rate
  },

  // 48-kHz AC-3 over S/PDIF
  {
    {
      sizeof(KSDATARANGE_AUDIO),
      0,
      0,
      0,
      STATICGUIDOF(KSDATAFORMAT_TYPE_AUDIO),
      STATICGUIDOF(KSDATAFORMAT_SUBTYPE_AC3_SPDIF),
      STATICGUIDOF(KSDATAFORMAT_SPECIFIER_WAVEFORMATEX)
    },
    2,       // Max number of channels
    16,      // Minimum number of bits per sample
    16,      // Maximum number of bits per channel
    48000,   // Minimum rate
    48000    // Maximum rate
  },
};
```

このコード例では、1番目と2番目のデータ範囲は、48 kHz と 44.1 kHz のサンプルレートで、WMA Pro over S/PDIF データ形式を指定します。 これら2つのオプションを使用すると、オーディオアプリケーションでは、これら2つのサンプルレートのどちらかで記録された WMA Pro オーディオストリームを再生できます。これは、外部デコーダーがサンプル速度も処理できることを前提としています。

WMA Pro 同期フレームサイズは 48 kHz と 44.1 kHz の両方で同じであり、両方のデータ範囲で同じ PCM パラメーター値 (2 チャネルと16ビット/チャネル) が使用されています。 PCM パラメーターを使用して、WMA Pro over S/PDIF および AC-3 over S/PDIF 形式のデータ範囲を指定する方法の詳細については、「[非 PCM ストリームの S/PDIF パススルー伝送](s-pdif-pass-through-transmission-of-non-pcm-streams.md)」を参照してください。

3番目のデータ範囲では、AC-3 over S/PDIF データ形式を指定します。 詳細については、「 [AC データ範囲の指定](specifying-ac-3-data-ranges.md)」を参照してください。

前の例では、Microsoft Windows 2000 SP2 および Windows 98 SE + 修正プログラムでは、DirectSound で、非 PCM WMA Pro over S/PDIF および AC 3 over S/PDIF 形式を処理することはできません。 この機能を有効にするには、サンプルコードを変更する必要があります。これにより、指定子を使用する3つのデータ範囲\_KSDATAFORMAT\_指定子を使用するようになります。2番目のデータ範囲は、を使用する点を除いて同じである必要があります。指定子 KSDATAFORMAT\_指定子は、代わりに DSOUND を\_します。 例については、「 [AC データ範囲の指定](specifying-ac-3-data-ranges.md)」を参照してください。

 

 




