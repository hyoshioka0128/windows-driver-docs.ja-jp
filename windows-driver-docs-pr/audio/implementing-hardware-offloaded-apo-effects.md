---
title: APO 効果をオフロードするハードウェアの実装
description: オーディオ処理オブジェクト (APOs) のハードウェアオフロードによって、パフォーマンスが向上するだけでなく、省電力も得られます。
ms.assetid: 159DFFD2-2434-4EDC-A83C-455BA80F74C6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e24d0d5a9b9959fa165aa10a6f7a5910d301bf3
ms.sourcegitcommit: 7a69c2e0abf91a57407b13a30faf24925f677970
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85829027"
---
# <a name="hardware-offloaded-apo-effects"></a>ハードウェアオフロード APO 効果

Windows 10 バージョン1511以降では、オーディオ処理オブジェクト (APOs) のオフロードがサポートされています。 パフォーマンスを向上させることができるだけでなく、ハードウェアオフロード APOs を使用する場合にも、大幅な電力を節約できます。

ハードウェアオフロードの再生中に、2種類の APOs を読み込むことができます。

1. ストリーム効果のオフロード (OSFX)
2. オフロードモードの効果 (OMFX)

## <a name="hardware-offloaded-apo-effects-overview"></a>ハードウェアオフロード APO 効果の概要

### <a name="hardware-offloaded-audio-processing-and-hardware-offloaded-apos"></a>ハードウェアオフロードオーディオ処理とハードウェアオフロード APOs

Windows 8 では、オーディオエンジンは、コンピューターのメインオーディオシステムとは別のハードウェアデバイスにオフロードされたオーディオストリームで動作するように再設計されています。 これは、ハードウェアオフロードと呼ばれます。 詳細については、「[ハードウェアオフロードオーディオ処理](hardware-offloaded-audio-processing.md)」を参照してください。

ハードウェアオフロード機能は、主にバッファーサイズが大きい低電力のシナリオを対象としています。 たとえば、サポートされているシステムで低電力オーディオ (LPA) の再生中には、オーディオバッファーサイズまたは周期性が1秒に設定されており、CPU が小さなバッファーを処理するために頻繁にウェイクアップしないようにします (たとえば、10ミリ秒ごと)。

ハードウェアオフロードを使用してハードウェアオフロードを実装すると、電力効率を最大限に高めることができます。

次の図は、オーディオ処理オブジェクトのアーキテクチャを示しています。 図の右側には、ハードウェアオフロード OSFX と OMFX 効果に通信するアプリケーションが示されています。

![sfx mfx に対するアプリケーション呼び出しを示すオーディオドライバーのアーキテクチャと、ドライバーおよびオーディオハードウェアに対して呼び出す efx 効果](images/audio-hardware-offloaded-apo-overview.png)

## <a name="implementing-hardware-offloaded-apo-effects"></a>APO 効果をオフロードするハードウェアの実装

ハードウェアオフロード APO は、「[オーディオ処理オブジェクトのアーキテクチャ](audio-processing-object-architecture.md)」および「[オーディオ処理オブジェクトの実装](implementing-audio-processing-objects.md)」で説明されているものと同じ基本的な要件と設計の原則に従う必要があります。

### <a name="supported-audio-format-implementation-guidelines"></a>サポートされているオーディオ形式の実装ガイドライン

ハードウェアオフロードの場合、サポートされているオーディオ形式に追加の考慮事項が必要になります。

各 APO は[**Iaudioprocessingobject:: IsInputFormatSupported**](https://docs.microsoft.com/windows/desktop/api/audioenginebaseapo/nf-audioenginebaseapo-iaudioprocessingobject-isinputformatsupported)メソッドを実装しています。このメソッドは、オーディオグラフの作成中に使用され、出力オーディオ形式と、任意の形式変換が必要かどうかを判断します。

```cpp
HRESULT IsInputFormatSupported(
  [in, optional]  IAudioMediaType *pOppositeFormat,
  [in, optional]  IAudioMediaType *pRequestedInputFormat,
  [out, optional] IAudioMediaType **ppSupportedInputFormat
);
```

オフロードレンダリングエンドポイントは、ホスト/システムの pin レンダリングでサポートされる既定の形式を含む、さまざまな形式をサポートできます。 オフロード APO は、(サポートされている形式の) レンダリングストリームが追加の形式変換を実行する必要がないように、これらすべての形式をサポートする必要があります。

オフロード SFX は、形式変換を実装し、より広範な形式を受け入れることができます。 たとえば、オフロード SFX がヘッドホンの仮想化を提供している場合 (つまり、5.1 チャネルオーディオをステレオに変換する場合)、 \_ このメソッドでは、適切な入力/出力のペアに対して S OK を返す必要があります。

オフロードの SFX では、サポートされているオフロードピンの形式を確認し、サポート/機能の拡張を行う必要があります。

オフロード MFX は入力ストリームの形式を変更できませんが、オフロードエンドポイントによって提供されるさまざまな形式をサポートし、不要な形式変換を排除する必要があります。

オフロードピンでのレンダリング中は、そのピンでアクティブになっているストリームが1つだけであるため、ストリームが混在していません。 そのため、ストリームレベルとモードレベルの両方でオーディオを処理する必要はありません。 そのため、ストリームの効果とモードの両方の効果として、オーディオ効果を有効にする必要がない場合があります。 オフロードエンドポイントは、より多くのストリームをサポートします。また、システムの処理アーキテクチャによっては、オフロード処理を SFX/MFX に分割する必要がある場合があります。

### <a name="inf-file-entries"></a>INF ファイルのエントリ

次の INF ファイルエントリを実装して、オフロード再生中に読み込む効果を定義します。 INF ファイルのプロパティキーは、オーディオエンドポイントビルダーに対して、オフロード APOs の Clsid を effects プロパティストアに設定するように指示します。 この情報は、上位レベルのアプリに対してどのような効果が適用されているかを通知するために使用されるオーディオグラフを構築するために使用されます。

|プロパティキー|GUID|
|----|----|
| [PKEY \_ FX \_ オフロード \_ StreamEffectClsid](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-fx-offload-streameffectclsid)                                                  | {D04E05A6-594B-4FB6-A80D-01AF5EED7D1D}、11 |
| [PKEY \_ FX \_ オフロード \_ ModeEffectClsid](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-fx-offload-modeeffectclsid)                                                      | {D04E05A6-594B-4FB6-A80D-01AF5EED7D1D}、12 |
| [\_ \_ \_ \_ ストリーミングでサポートされている PKEY SFX Offload processingmodes \_ \_](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-sfx-offload-processingmodes-supported-for-streaming) | {D3993A3F-99C2-4402-B5EC-A92A0367664B}、11 |
| [\_ \_ \_ \_ ストリーミングでサポートされる PKEY mfx オフロード \_ の processingmodes \_](https://docs.microsoft.com/windows-hardware/drivers/audio/pkey-mfx-offload-processingmodes-supported-for-streaming) | {D3993A3F-99C2-4402-B5EC-A92A0367664B}、12 |

## <a name="related-topics"></a>関連項目

[オーディオ処理オブジェクトの実装](implementing-audio-processing-objects.md)  
[Windows オーディオ処理オブジェクト](windows-audio-processing-objects.md)  
