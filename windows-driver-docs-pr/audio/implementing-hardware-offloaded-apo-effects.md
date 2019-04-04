---
title: APO 効果をオフロードするハードウェアの実装
description: オーディオ処理オブジェクト (APOs) のハードウェアのオフロードには、可能なパフォーマンスの向上、省電力が提供します。
ms.assetid: 159DFFD2-2434-4EDC-A83C-455BA80F74C6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 003ed70c695725b7a1713e910edc8de0835f2c04
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578661"
---
# <a name="implementing-hardware-offloaded-apo-effects"></a>APO 効果をオフロードするハードウェアの実装


Windows 10 でバージョン 1511 以降がオーディオ処理オブジェクト (APOs) のオフロードがサポートされています。 に加えて可能なパフォーマンスの向上、重要な考えられる電源節約使用可能な場合は APOs をオフロードするハードウェアを使用します。

2 種類の APOs ハードウェア オフロード再生中に読み込むことができます。

1. Stream の効果 (OSFX) の負荷を軽減します。
2. モードの効果 (OMFX) の負荷を軽減します。



## <a name="span-idhardwareoffloadedapoeffectsoverviewspanspan-idhardwareoffloadedapoeffectsoverviewspanspan-idhardwareoffloadedapoeffectsoverviewspanhardware-offloaded-apo-effects-overview"></a><span id="Hardware_Offloaded_APO_Effects_Overview"></span><span id="hardware_offloaded_apo_effects_overview"></span><span id="HARDWARE_OFFLOADED_APO_EFFECTS_OVERVIEW"></span>ハードウェア オフロード APO 効果の概要


**ハードウェア オフロードされたオーディオ処理およびハードウェア オフロード APOs**

Windows 8 でオーディオ エンジンが再設計されましたとは別ですが、コンピューターのメインのオーディオ システムに接続されているハードウェア デバイスにオフロードされたオーディオのストリームを使用します。 これはハードウェアのオフロードと呼ばれます。 詳細については、[Hardware-Offloaded オーディオ処理](hardware-offloaded-audio-processing.md)を参照してください。

ハードウェアのオフロード機能は主に、バッファー サイズの大きな低電力のシナリオの対象とします。 たとえば、対応システムでは、低電力オーディオ (以下) の再生中に、オーディオのバッファー サイズまたは周期性は 1 秒に設定、CPU がウェイク アップ頻繁に (たとえば、10 ミリ秒ごと) で小さなバッファーを処理するように。

ハードウェア オフロードされたオーディオ処理と共にハードウェア オフロード APOs を実装するには、電源効率を最大化する機能が提供します。

次の図は、オーディオ処理オブジェクト アーキテクチャを示します。 図の右側にあるは、ハードウェアに通信するアプリケーションは、オフロード OSFX と OMFX 効果を示しています。

![sfx を呼び出すことをアプリケーションにドライバーやオーディオ ハードウェアを呼び出して mfx と efx の効果を示すオーディオ ドライバーのアーキテクチャ](images/audio-hardware-offloaded-apo-overview.png)

## <a name="span-idimplementinghardwareoffloadedapoeffectsspanspan-idimplementinghardwareoffloadedapoeffectsspanspan-idimplementinghardwareoffloadedapoeffectsspanimplementing-hardware-offloaded-apo-effects"></a><span id="Implementing_Hardware_Offloaded_APO_Effects"></span><span id="implementing_hardware_offloaded_apo_effects"></span><span id="IMPLEMENTING_HARDWARE_OFFLOADED_APO_EFFECTS"></span>APO 効果をオフロードするハードウェアを実装します。


ハードウェアのオフロード APO する必要があります同じ基本的な要件に従い、および設計原則で説明されている[オーディオ処理オブジェクト アーキテクチャ](audio-processing-object-architecture.md)と[オーディオ処理オブジェクトを実装する](implementing-audio-processing-objects.md)します。

**オーディオ形式の実装のガイドラインのサポート**

ハードウェア オフロード、APOs、サポートされているオーディオ形式をいくつか追加の考慮事項を与える必要があります。

各 APO 実装[ **IAudioProcessingObject::IsInputFormatSupported** ](https://msdn.microsoft.com/library/windows/hardware/ff536511)出力オーディオ形式と変換する任意の形式かどうかを判断するオーディオのグラフの構築時に使用されるメソッドは、必要です。

```cpp
HRESULT IsInputFormatSupported(
  [in, optional]  IAudioMediaType *pOppositeFormat,
  [in, optional]  IAudioMediaType *pRequestedInputFormat,
  [out, optional] IAudioMediaType **ppSupportedInputFormat
);
```

オフロード レンダー エンドポイントは、さまざまなホスト/システム暗証番号 (pin) のレンダリングでサポートされている既定の形式を含む形式をサポートできます。 (サポートされている形式) でレンダリング ストリームは、追加の形式変換を経由する必要があるないようにこれらすべての形式、オフロード APO をサポートする必要があります。

SFX をオフロードでは、形式変換を実装でき、広い範囲の形式をそのまま使用することができます。 たとえば、オフロード SFX では、ヘッドホンによる立体音響仮想化 (つまり、ステレオ チャネル オーディオを 5.1 を変換するなど) を提供する場合が返されます S\_このメソッドで適切な入力/出力のペアには、[ok] です。

SFX をオフロードは、オフロード サポートされている pin の形式を確認し、サポート/機能を拡張する必要があります。

オフロード MFX、入力ストリームの形式を変更することはできませんが、まだをオフロード エンドポイントによって提供される形式のさまざまなサポートし、不要な形式の変換を削除する必要があります。

オフロード pin でのレンダリング中に 1 つのみのストリームがその pin でアクティブになって、したがってされませんストリームが混在するとします。 そのため、ストリーム レベルとモードのレベルの両方でオーディオを処理する必要はありません。 したがってオーディオ効果は、ストリーム効果とモードの影響の両方として有効にすることがあります必要ありません。 オフロードされたエンドポイントは複数のストリームをサポートし、システムの処理アーキテクチャによって処理のオフロードが SFX/MFX に考慮する必要があります。 

**INF ファイルのエントリ**

オフロード再生中に読み込まれる効果を定義する次の INF ファイルのエントリを実装します。 INF ファイルのプロパティのキーは、効果のプロパティ ストアにオフロード APOs の Clsid を設定するオーディオ エンドポイント ビルダーに指示します。 この情報は、どのような効果が適用されて、上位レベル アプリを通知するために使用されるオーディオ、グラフの作成に使用されます。

|                                                                                                                                  |                                           |
|----------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------|
| **プロパティのキー**                                                                                                                 | **GUID**                                  |
| [鍵\_FX\_オフロード\_StreamEffectClsid](https://msdn.microsoft.com/library/windows/hardware/mt604869)                                                  | {D04E05A6-594B-4FB6-A80D-01AF5EED7D1D} 11 |
| [PKEY\_FX\_Offload\_ModeEffectClsid](https://msdn.microsoft.com/library/windows/hardware/mt604868)                                                      | {D04E05A6-594B-4FB6-A80D-01AF5EED7D1D} 12 |
| [鍵\_SFX\_オフロード\_ProcessingModes\_サポート\_の\_ストリーミング](https://msdn.microsoft.com/library/windows/hardware/mt604871) | {D3993A3F-99C2-4402-B5EC-A92A0367664B},11 |
| [鍵\_MFX\_オフロード\_ProcessingModes\_サポート\_の\_ストリーミング](https://msdn.microsoft.com/library/windows/hardware/mt604870) | {D3993A3F-99C2-4402-B5EC-A92A0367664B},12 |

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック
[オーディオ処理オブジェクトの実装](implementing-audio-processing-objects.md)  
[Windows オーディオ処理オブジェクト](windows-audio-processing-objects.md)  



