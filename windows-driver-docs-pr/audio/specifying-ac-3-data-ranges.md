---
title: AC-3 データ範囲の指定
description: AC-3 データ範囲の指定
ms.assetid: 87d59554-43fa-4d61-9829-c38691d0a525
keywords:
- S/PDIF パススルー WDK オーディオ
- AC-3-フェールオーバー-S/PDIF 形式の WDK オーディオ
- PCM 以外のオーディオ形式 WDK
- 非 PCM オーディオの形式、WDK S/PDIF
- WMA Pro WDK オーディオ
- Ac-3 WDK オーディオ
- Sony/Philips デジタル インターフェイス
- データ範囲の WDK オーディオ、ac-3
- 非 PCM オーディオの形式、WDK ac-3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c6b9480e9ad1d81af5d547f57bbe1f0f4ddfc70d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328620"
---
# <a name="specifying-ac-3-data-ranges"></a>AC-3 データ範囲の指定


## <span id="specifying_ac_3_data_ranges"></span><span id="SPECIFYING_AC_3_DATA_RANGES"></span>


ヘッダー ファイル Mmreg.h 0x0092 AC-3-フェールオーバー-S/PDIF を wave 形式のタグの値を定義します。

```cpp
    #define WAVE_FORMAT_DOLBY_AC3_SPDIF  0x0092
```

0x0240 および 0x0241、Wave 形式のタグが 0x0092 と同義にあり、多くの DVD アプリケーションとして同じ 3 つのタグを処理します。 ただし、冗長性をなくすため、ドライバーとアプリケーションする必要があります 0x0092 タグのみをサポート (および 0x0240 および 0x0241 タグをサポートしていません)。

定義を使用して wave 形式のタグの観点から対応する形式とサブタイプの GUID を指定できます\_WAVEFORMATEX\_ヘッダーから GUID マクロ ファイル Ksmedia.h は次のようにします。

```cpp
  #define KSDATAFORMAT_SUBTYPE_AC3_SPDIF    \
                      DEFINE_WAVEFORMATEX_GUID(WAVE_FORMAT_DOLBY_AC3_SPDIF)
```

次のコード例は、WaveCyclic または WavePci ミニポート ドライバーを指定する方法を示しています、 [ **KSDATARANGE\_オーディオ**](https://msdn.microsoft.com/library/windows/hardware/ff537096) AC-3-フェールオーバー-S/PDIF 形式をサポートする、暗証番号 (pin) のエントリをテーブルします。

```cpp
static KSDATARANGE_AUDIO PinDataRangesAC3Stream[] =
{
  // 48-kHz AC-3 over S/PDIF
  {
    {
      sizeof(KSDATARANGE_AUDIO),
      0,
      0,
      0,
      STATICGUIDOF(KSDATAFORMAT_TYPE_AUDIO),
      STATICGUIDOF(KSDATAFORMAT_SUBTYPE_DOLBY_AC3_SPDIF),
      STATICGUIDOF(KSDATAFORMAT_SPECIFIER_WAVEFORMATEX)
    },
    2,     // Max number of channels
    16,    // Minimum number of bits per sample
    16,    // Maximum number of bits per channel
    48000, // Minimum rate
    48000  // Maximum rate
  },

  // If you do not include this second data range (which is identical
  // to the first except for the value KSDATAFORMAT_SPECIFIER_DSOUND),
  // then your non-PCM pin is not seen by DirectSound on Windows 98 SE
  // or Windows 2000, regardless of the DirectX version or whether a
  // hotfix or service pack is installed.
  {
    {
      sizeof(KSDATARANGE_AUDIO),
      0,
      0,
      0,
      STATICGUIDOF(KSDATAFORMAT_TYPE_AUDIO),
      STATICGUIDOF(KSDATAFORMAT_SUBTYPE_DOLBY_AC3_SPDIF),
      STATICGUIDOF(KSDATAFORMAT_SPECIFIER_DSOUND)
    },
    2,     // Max number of channels
    16,    // Minimum number of bits per sample
    16,    // Maximum number of bits per channel
    48000, // Minimum rate
    48000  // Maximum rate
  }
};
```

上記の表に、2 番目のデータ範囲エントリは、Windows 2000 sp2、および Microsoft Windows 98 SE + 修正プログラムで非 PCM AC-3-フェールオーバー-S/PDIF 形式を処理するために、DirectSound を有効にする必要があります。

KSDATAFORMAT ミニポート ドライバーを指定する各データ範囲の\_指定子\_WAVEFORMATEX、ポートのドライバーを自動的に追加 KSDATAFORMAT で指定されている 2 番目のデータ範囲\_指定子\_DSOUND がそれ以外の場合、最初と同じです。 (これを確認するにを使用して、 [KsStudio ユーティリティ](ksstudio-utility.md)データ範囲の一覧を表示します)。ポート ドライバーを Windows 2000 および Windows 98 では、KSDATAFORMAT を作成します\_指定子\_DSOUND バージョン KSDATAFORMAT のみのデータ範囲の\_サブタイプ\_PCM ために、フォーマットする前に、DirectSound のバージョンDirectSound 8 では、PCM のみをサポートします。 この制限は、Windows XP では削除し、以降と Windows me で ただし、Windows 2000 SP2 または Windows 98 SE、ホット フィックス プレゼンテーションでは削除されませんし、これらの Windows バージョンを DirectSound で非 PCM をサポートするドライバーが明示的に一覧表示は、各 PCM 以外のデータの形式 - KSDATAFORMATで1つの2つのデータ範囲\_指定子\_、WAVEFORMATEX、もう KSDATAFORMAT\_指定子\_DSOUND します。

説明したよう[非 PCM ストリームのパススルー送信を S/PDIF](s-pdif-pass-through-transmission-of-non-pcm-streams.md)、2 つ AC-3-フェールオーバー-S/PDIF データの範囲両方は、次の PCM パラメーターを使用: 2 つのチャネルとチャネルあたり 16 ビット。

 

 




