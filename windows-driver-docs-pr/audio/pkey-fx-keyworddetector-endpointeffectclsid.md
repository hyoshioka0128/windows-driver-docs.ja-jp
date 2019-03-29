---
title: 鍵\_FX\_KeywordDetector\_EndpointEffectClsid
description: Windows 10 以降、鍵の\_FX\_KeywordDetector\_EndpointEffectClsid プロパティのキーは、インプレース キーワード detector 終点効果 (EFX) を識別します。
ms.assetid: 2D776DB4-A317-4097-B188-65CA495D0F89
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb0ed082502892fde4d872e146c01e613359a8d5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574462"
---
# <a name="pkeyfxkeyworddetectorendpointeffectclsid"></a>鍵\_FX\_KeywordDetector\_EndpointEffectClsid


Windows 10 以降では、**鍵\_FX\_KeywordDetector\_EndpointEffectClsid**プロパティのキーは、インプレース キーワード detector 終点効果 (EFX) を識別します。 ドライバー開発者は、キーワード detector の暗証番号 (pin) のドライバーをサポートする単一のサポートされている処理モードを指定する必要があります。

INF ファイルのプロパティのキーでは、オーディオ エンドポイント ビルダー エンドポイント APOs の効果のプロパティ ストアに、Clsid を設定するように指示します。 この情報は、どのような効果が適用されて、上位レベル アプリを通知するために使用されるオーディオ、グラフの作成に使用されます。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>サンプルの INF ファイル


INF ファイルでは、そのデバイスの追加レジストリ セクションで、エンドポイントのオーディオ デバイスの既定の形式を指定します。 INF の次の例では、文字列と、レジストリにエンドポイント キーワード detector 効果の APO を読み込みます - レジストリの追加セクションを示します。

```inf
[Strings]
PKEY_FX_KeywordDetector_EndpointEffectClsid = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},10"
...
; Driver developers should replace this CLSIDs with that of their own APO
FX_KEYWORD_ENDPOINT_CLSID               = "{00000000-0000-0000-0000-000000000000}"
...
[SWAPAPO.I.Association0.AddReg]
HKR,"FX\\0",%PKEY_FX_KeywordDetector_EndpointEffectClsid%,,%FX_KEYWORD_ENDPOINT_CLSID%
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Media クラス INF の拡張機能](media-class-inf-extensions.md)

 

 






