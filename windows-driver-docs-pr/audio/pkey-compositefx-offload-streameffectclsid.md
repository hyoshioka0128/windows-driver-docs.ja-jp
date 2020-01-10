---
title: PKEY\_CompositeFX\_Offload\_StreamEffectClsid
description: Windows 10 バージョン1803以降では、PKEY\_CompositeFX\_Offload\_StreamEffectClsid プロパティキーは、ドライバーでサポートされているストリーム効果 (SFX) を識別します。
ms.date: 01/07/2020
ms.localizationpriority: medium
ms.openlocfilehash: 97c5a1f9bee50d903f73e3b424791665ddc72864
ms.sourcegitcommit: 09a1ef35029216ce98510ae8794c957157d9688e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/08/2020
ms.locfileid: "75727777"
---
# <a name="pkey_compositefx_offload_streameffectclsid"></a>PKEY\_CompositeFX\_Offload\_StreamEffectClsid

Windows 10 バージョン1803以降では、 **PKEY\_CompositeFX\_offload\_StreamEffectClsid**プロパティキーによって、オフロードの再生中に読み込まれるドライバーでサポートされているストリーム効果 (SFX) が識別されます。 ドライバーの開発者は、ドライバーがオフロード pin に対してサポートする、サポートされているストリームの効果の一覧を指定する必要があります。

このプロパティキーは、 [PKEY\_FX\_Offload\_StreamEffectClsid](pkey-fx-offload-streameffectclsid.md) property キーと同じですが、1つの位置に複数の効果を与えるためにレジストリで reg 文字列として表現される複合型です。

INF ファイルのプロパティキーは、オフロード用に effects プロパティストアにストリーム効果の Clsid を設定するように、オーディオエンドポイントビルダーに指示します。 この情報は、上位レベルのアプリに対してどのような効果が適用されているかを通知するために使用されるオーディオグラフを構築するために使用されます。

## <a name="span-idinf_file_samplespanspan-idinf_file_samplespanspan-idinf_file_samplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>INF ファイルのサンプル

INF ファイルでは、そのデバイスの [レジストリの追加] セクションでのオーディオ処理モード効果の設定を指定します。 次の INF の例は、レジストリにサポートされているストリーミング処理モードを読み込む文字列と追加レジストリセクションを示しています。

```inf
[Strings]
PKEY_CompositeFX_Offload_StreamEffectClsid   = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},19"
...
; Driver developers should replace this CLSIDs with that of their own APO
SWAP_FX_MODE_CLSID      = "{00000000-0000-0000-0000-000000000000}"
DELAY_FX_STREAM_CLSID   = "{00000000-0000-0000-0000-000000000000}"
...

[SWAPAPO.I.Association0.AddReg]
HKR,FX\0,%PKEY_CompositeFX_Offload_StreamEffectClsid%,0x00010000,%SWAP_FX_MODE_CLSID%,%DELAY_FX_MODE_CLSID%


```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[メディアクラスの INF 拡張機能](media-class-inf-extensions.md)
