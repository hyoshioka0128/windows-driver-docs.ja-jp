---
title: WMA Pro データ範囲の指定
description: WMA Pro データ範囲の指定
ms.assetid: c7e9bc68-cec2-4a34-9ef0-ce3c9a4cc987
keywords:
- S/PDIF パススルー WDK オーディオ
- WMA Pro オーバー-S/PDIF 形式の WDK オーディオ
- PCM 以外のオーディオ形式 WDK
- 非 PCM オーディオの形式、WDK S/PDIF
- WMA Pro WDK オーディオ
- Sony/Philips デジタル インターフェイス
- データ範囲 WDK オーディオ、WMA Pro
- 非 PCM のオーディオ形式 WDK、WMA Pro
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 757c87ccc2234773b6570bde8b4a0e5f56cc0ffe
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328616"
---
# <a name="specifying-wma-pro-data-ranges"></a>WMA Pro データ範囲の指定


## <span id="specifying_wma_pro_data_ranges"></span><span id="SPECIFYING_WMA_PRO_DATA_RANGES"></span>


ヘッダー ファイル Mmreg.h 0x0164 WMA Pro-オーバー-S/PDIF を wave 形式のタグの値を定義します。

```cpp
  #define WAVE_FORMAT_WMASPDIF  0x0164
```

定義を使用して wave 形式のタグの観点から対応する形式とサブタイプの GUID を指定できます\_WAVEFORMATEX\_ヘッダーから GUID マクロ ファイル Ksmedia.h は次のようにします。

```cpp
  #define KSDATAFORMAT_SUBTYPE_WMA_SPDIF    \
                      DEFINE_WAVEFORMATEX_GUID(WAVE_FORMAT_WMASPDIF)
```

次のコード例は、WaveCyclic または WavePci ミニポート ドライバーを指定する方法を示しています、 [ **KSDATARANGE\_オーディオ**](https://msdn.microsoft.com/library/windows/hardware/ff537096) WMA Pro-オーバー-S/PDIF をサポートする、暗証番号 (pin) のエントリをテーブルとAC-3-フェールオーバー-S/PDIF 形式:

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

このコード例では、最初と 2 番目のデータの範囲は、48 kHz と 44.1 kHz のサンプル レートで WMA Pro オーバー-S/PDIF データ形式を指定します。 これら 2 つのオプションでは、オーディオのアプリケーションはこれら 2 つのサンプル レートと仮定すると、外部のデコーダーの場合、サンプル速度も処理のいずれかで記録された WMA Pro オーディオ ストリームを再生できます。

WMA Pro 同期フレーム サイズは、48 kHz と 44.1 kHz の両方で同じ両方のデータ範囲を使用して、同じ PCM パラメーター値: 2 つのチャネルとチャネルの 16 ビット/。 WMA Pro-オーバー-S/PDIF と AC-3-フェールオーバー-S/PDIF 形式のデータ範囲を指定する PCM パラメーターの使用については、次を参照してください。[非 PCM ストリームのパススルー送信を S/PDIF](s-pdif-pass-through-transmission-of-non-pcm-streams.md)します。

3 番目のデータ範囲には、AC-3-フェールオーバー-S/PDIF のデータ形式を指定します。 詳細については、次を参照してください。 [ac-3 データ範囲を指定する](specifying-ac-3-data-ranges.md)します。

前の例は、PCM 以外の WMA Pro-オーバー-S/PDIF と Microsoft Windows 2000 SP2 および Windows 98 SE + 修正プログラムの AC-3-フェールオーバー-S/PDIF 形式を処理するために、DirectSound を有効になりません。 この機能を有効にするサンプル コードが 3 つのデータ範囲の各 KSDATAFORMAT 指定子を使用するように変更する必要は\_指定子\_WAVEFORMATEX、2 番目のデータ範囲を含めることは以外と等しいKSDATAFORMAT 指定子を使用している\_指定子\_DSOUND 代わりにします。 例については、次を参照してください。 [ac-3 データ範囲を指定する](specifying-ac-3-data-ranges.md)します。

 

 




