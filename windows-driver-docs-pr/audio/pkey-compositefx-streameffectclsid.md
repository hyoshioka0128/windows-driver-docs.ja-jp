---
title: 鍵\_CompositeFX\_StreamEffectClsid
description: Windows 10 バージョン 1803 以降鍵で\_FX\_StreamEffectClsid プロパティのキーは、ドライバーでサポートされているストリーム効果 (SCompositeFX) を識別します。 ドライバー開発者は、そのドライバーがサポートするストリームがサポートされている効果の一覧を指定する必要があります。
ms.date: 11/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: c9c37a48e93ed438705e240bfb29869d17329b84
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332183"
---
# <a name="pkeycompositefxstreameffectclsid"></a>鍵\_CompositeFX\_StreamEffectClsid


Windows 10 バージョン 1803 以降では、**鍵\_CompositeFX\_StreamEffectClsid**プロパティのキーは、ドライバーでサポートされているストリーム効果 (SCompositeFX) を識別します。 ドライバー開発者は、そのドライバーがサポートするストリームがサポートされている効果の一覧を指定する必要があります。

このプロパティのキーのと同じですが、[鍵\_FX\_StreamEffectClsid](pkey-fx-streameffectclsid.md)プロパティのキーでは 1 つの位置に複数の効果を許可するレジストリの reg 複数文字列として表現されるコンポジット。

INF ファイルのプロパティのキーは、効果のプロパティ ストアにエンドポイント APOs の Clsid を設定するオーディオ エンドポイント ビルダーに指示します。 この情報は、どのような効果が適用されて、上位レベル アプリを通知するために使用されるオーディオ、グラフの作成に使用されます。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>サンプルの INF ファイル


INF ファイルでは、そのデバイスの追加レジストリ セクションでは、エンドポイントのオーディオ デバイスの設定を指定します。 文字列とレジストリを追加のセクションでは、レジストリにストリームの効果の APO をロードする INF の次の例を示しています。

```inf
[Strings]
PKEY_CompositeFX_StreamEffectClsid   = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},13"
...
; Driver developers should replace this CLSIDs with that of their own APO
SWAP_FX_MODE_CLSID      = "{00000000-0000-0000-0000-000000000000}"
DELAY_FX_STREAM_CLSID   = "{00000000-0000-0000-0000-000000000000}"
...
 
[SWAPAPO.I.Association0.AddReg]
HKR,FX\0,%PKEY_CompositeFX_StreamEffectClsid%,0x00010000,%SWAP_FX_MODE_CLSID%,%DELAY_FX_MODE_CLSID%

```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Media クラス INF の拡張機能](media-class-inf-extensions.md)

 

 






