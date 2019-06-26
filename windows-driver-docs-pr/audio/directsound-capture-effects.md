---
title: DirectSound キャプチャ効果
description: DirectSound キャプチャ効果
ms.assetid: 5dcadcea-0b6a-447d-828d-a7f256f97088
keywords:
- DirectSound WDK オーディオ キャプチャの効果
- アコースティック エコー キャンセル WDK オーディオ
- ノイズの抑制 WDK オーディオ
- AEC WDK オーディオ
- 効果の WDK オーディオをキャプチャします。
- 全二重アプリケーション WDK オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c2146e41b43ca6fbaadc28fe5ec12e595fb5449
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360140"
---
# <a name="directsound-capture-effects"></a>DirectSound キャプチャ効果


## <span id="directsound_capture_effects"></span><span id="DIRECTSOUND_CAPTURE_EFFECTS"></span>


DirectSound 8 では、一部の新機能を有効にすると、サード パーティ製の効果を制御するオーディオ キャプチャ中に追加します。 これと DirectSound の以降のバージョンは、次の 2 つのキャプチャの効果をサポートします。

-   アコースティック エコー キャンセル (AEC)

-   ノイズの抑制 (NS)

電話会議などの完全な双方向オーディオ アプリケーションで、スピーカーから出力されるレンダリングのストリームの中にこだまキャプチャ ストリームを生成するマイクで取得されます。 ルームまたはその他の物理的な環境でのサウンドの反射を特徴付ける後は、全二重システムは、キャプチャ ストリームに追加されるエコー アウトをキャンセルするのにレンダリング ストリームを監視するのに AEC を使用します。 システムは、ノイズのスパイクを検出し、ストリームから削除する NS を使用してキャプチャ ストリームの品質をさらに向上できます。

全二重 DirectSound のアプリケーションを使用できます、 **IDirectSoundCaptureFXAec**と**IDirectSoundCaptureFXNoiseSuppress** AEC および NS 効果を制御するインターフェイス。 **IDirectSoundCaptureBuffer::GetObjectInPath**メソッドは、これらのインターフェイスを持つオブジェクトへのポインターを取得します。 **DirectSoundFullDuplexCreate**関数を作成、 **IDirectSoundCaptureBuffer**オブジェクト、および呼び出し元がこの関数に渡されるパラメーターは DSCEFFECTDESC 構造体の配列が含まれます。 配列には、キャプチャ バッファーで有効にするには効果を指定します。 **GuidDSCFXClass**配列内の各構造体のメンバーには、効果を指定する GUID が含まれています。AEC または NS します。 Guid ごと DirectSound 名前は、同じ GUID 値の KS 名と共に、次の表に表示されます。 詳細については、DirectX 8.0 SDK ドキュメントを参照してください。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">DirectSound GUID 名</th>
<th align="left">KS GUID 名</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>GUID_DSCFX_CLASS_AEC</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-acoustic-echo-cancel" data-raw-source="[&lt;strong&gt;KSNODETYPE_ACOUSTIC_ECHO_CANCEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-acoustic-echo-cancel)"><strong>KSNODETYPE_ACOUSTIC_ECHO_CANCEL</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p>GUID_DSCFX_CLASS_NS</p></td>
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-noise-suppress" data-raw-source="[&lt;strong&gt;KSNODETYPE_NOISE_SUPPRESS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/audio/ksnodetype-noise-suppress)"><strong>KSNODETYPE_NOISE_SUPPRESS</strong></a></p></td>
</tr>
</tbody>
</table>

 

Microsoft Windows XP 以降では、DirectSound のアプリケーションにオーディオ デバイスのハードウェア アクセラレータによるキャプチャの効果を公開できます。 さらに、AEC システム フィルター (Aec.sys) は、AEC と NS 効果のソフトウェア エミュレーションを提供します。

このセクションの残りの部分では、これらのトピックがについて説明します。

[ハードウェア アクセラレータによるキャプチャの効果を公開します。](exposing-hardware-accelerated-capture-effects.md)

[AEC システム フィルター](aec-system-filter.md)

 

 




