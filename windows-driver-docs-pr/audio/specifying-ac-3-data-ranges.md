---
title: AC-3 データ範囲の指定
description: AC-3 データ範囲の指定
ms.assetid: 87d59554-43fa-4d61-9829-c38691d0a525
keywords:
- S/PDIF パススルー WDK オーディオ
- AC-3-over S/PDIF 形式 WDK オーディオ
- 非 PCM 形式のオーディオ (WDK)
- PCM 以外のオーディオ形式 WDK、S/PDIF
- WMA Pro WDK オーディオ
- AC 3 WDK オーディオ
- Sony/お持ちのデジタルインターフェイス
- データ範囲 WDK オーディオ、AC-3
- PCM 以外のオーディオ形式 WDK、AC-3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e7fd788269cc3c571a72e1190875aa7e836c177
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830116"
---
# <a name="specifying-ac-3-data-ranges"></a>AC-3 データ範囲の指定


## <span id="specifying_ac_3_data_ranges"></span><span id="SPECIFYING_AC_3_DATA_RANGES"></span>


ヘッダーファイル Mmreg は、値0x0092 を定義します。この値は、AC-3-over S/PDIF の wave 形式タグになります。

```cpp
    #define WAVE_FORMAT_DOLBY_AC3_SPDIF  0x0092
```

波形式タグ0x0240 および0x0240 は0x0092 と同義であり、多くの DVD アプリケーションは同じように3つのタグを扱います。 ただし、冗長性を排除するために、ドライバーとアプリケーションはタグ0x0092 のみをサポートする必要があります (タグ0x0240 および0x0240 をサポートしていません)。

対応する形式とサブタイプの GUID は、次\_のように、ヘッダーファイルの WAVEFORMATEX\_GUID マクロを使用して、wave 形式のタグの観点から指定できます。

```cpp
  #define KSDATAFORMAT_SUBTYPE_AC3_SPDIF    \
                      DEFINE_WAVEFORMATEX_GUID(WAVE_FORMAT_DOLBY_AC3_SPDIF)
```

次のコード例は、WaveCyclic または WavePci ミニポートドライバーが、AC-3 over S/PDIF 形式をサポートしている pin に対して、 [**ksk の\_オーディオ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)テーブルエントリを指定する方法を示しています。

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

前の表の2番目のデータ範囲エントリは、DirectSound が Windows 2000 SP2 および Microsoft Windows 98 SE + 修正プログラムで、PCM 以外の AC 3 over S/PDIF 形式を処理できるようにするために必要です。

ミニポートドライバーで KSDATAFORMAT\_指定子\_WAVEFORMATEX が指定されているデータ範囲ごとに、DSOUND\_\_で指定された2番目のデータ範囲が自動的に追加されます。それ以外の場合は、最初のと同じです。 (これを確認するには、 [Ksstudio ユーティリティ](ksstudio-utility.md)を使用してデータ範囲の一覧を表示します)。Windows 2000 および Windows 98 では、DirectSound 8 より前の DirectSound バージョンでは PCM のみがサポートされているため、ポートドライバーは KSDATAFORMAT\_のサブタイプ\_PCM 形式に対してのみ、KSDATAFORMAT\_指定子\_DSOUND バージョンのデータ範囲を作成します。 この制限は、Windows XP 以降および Windows Me では削除されています。 ただし、windows 2000 SP2 または Windows 98 SE 用のホットフィックスパッケージでは削除されません。また、これらの Windows バージョンで DirectSound の PCM 以外のデータ範囲をサポートするには、ドライバーが PCM 以外のデータ形式ごとに2つのデータ範囲を明示的にリストする必要があり\_指定子\_WAVEFORMATEX、および KSDATAFORMAT\_指定子を持つ別の指定子\_DSOUND です。

「[非 PCM ストリームの s/PDIF パススルー伝送](s-pdif-pass-through-transmission-of-non-pcm-streams.md)」で説明されているように、2つの AC-3 over S/pdif データ範囲では、2つのチャネルと、チャネルあたり16ビットの両方の pcm パラメーターが使用されます。

 

 




