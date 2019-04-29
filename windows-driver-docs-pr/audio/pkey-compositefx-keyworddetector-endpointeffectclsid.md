---
title: 鍵\_CompositeFX\_KeywordDetector\_EndpointEffectClsid
description: Windows 10 バージョン 1803 以降鍵で\_CompositeFX\_KeywordDetector\_EndpointEffectClsid プロパティのキーは、インプレース キーワード detector 終点効果 (EFX) を識別します。
ms.date: 11/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0b052f997c2b9d898ccb77f05f99eaad312e70ae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332199"
---
# <a name="pkeycompositefxkeyworddetectorendpointeffectclsid"></a>鍵\_CompositeFX\_KeywordDetector\_EndpointEffectClsid

Windows 10 バージョン 1803 以降では、**鍵\_CompositeFX\_KeywordDetector\_EndpointEffectClsid**プロパティのキーは、インプレース キーワード detector 終点効果 (EFX) を識別します。 ドライバー開発者は、キーワード detector の暗証番号 (pin) のドライバーをサポートする単一のサポートされている処理モードを指定する必要があります。

このプロパティのキーのと同じですが、[鍵\_FX\_KeywordDetector\_EndpointEffectClsid](pkey-fx-keyworddetector-endpointeffectclsid.md)プロパティのキーが、許可するレジストリの reg 複数文字列として表される複合1 つの位置に複数の効果。

INF ファイルのプロパティのキーでは、オーディオ エンドポイント ビルダー エンドポイント APOs の効果のプロパティ ストアに、Clsid を設定するように指示します。 この情報は、どのような効果が適用されて、上位レベル アプリを通知するために使用されるオーディオ、グラフの作成に使用されます。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>サンプルの INF ファイル

INF ファイルでは、そのデバイスの追加レジストリ セクションで、エンドポイントのオーディオ デバイスの既定の形式を指定します。 INF の次の例では、文字列と、レジストリにエンドポイント キーワード detector 効果 APO を読み込みます - レジストリの追加セクションを示します。

```inf
[Strings]
PKEY_CompositeFX_KeywordDetector_EndpointEffectClsid = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},18"
...
; Driver developers should replace this CLSIDs with that of their own APO
SWAP_FX_MODE_CLSID      = "{00000000-0000-0000-0000-000000000000}"
DELAY_FX_STREAM_CLSID   = "{00000000-0000-0000-0000-000000000000}"
...
 
[SWAPAPO.I.Association0.AddReg]
HKR,FX\0,%PKEY_CompositeFX_KeywordDetector_EndpointEffectClsid%,0x00010000,%SWAP_FX_MODE_CLSID%,%DELAY_FX_MODE_CLSID%

```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Media クラス INF の拡張機能](media-class-inf-extensions.md)

 

 






