---
title: 鍵\_FX\_EndpointEffectClsid
description: Windows 8.1 以降、鍵で\_FX\_EndpointEffectClsid プロパティのキーは、インプレース終点効果 (EFX) を識別します。 ドライバー開発者は、そのドライバーがサポートするサポートされている処理モードの一覧を指定する必要があります。
ms.assetid: 19E92978-12DE-4B0E-A386-024B88A64B39
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22811ba13a6b449e237f939e087280b01887e20c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332140"
---
# <a name="pkeyfxendpointeffectclsid"></a>鍵\_FX\_EndpointEffectClsid


Windows 8.1 以降では、**鍵\_FX\_EndpointEffectClsid**プロパティのキーは、インプレース終点効果 (EFX) を識別します。 ドライバー開発者は、そのドライバーがサポートするサポートされている処理モードの一覧を指定する必要があります。

INF ファイルのプロパティのキーでは、オーディオ エンドポイント ビルダー エンドポイント APOs の効果のプロパティ ストアに、Clsid を設定するように指示します。 この情報は、どのような効果が適用されて、上位レベル アプリを通知するために使用されるオーディオ、グラフの作成に使用されます。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>サンプルの INF ファイル


INF ファイルでは、そのデバイスの追加レジストリ セクションで、エンドポイントのオーディオ デバイスの既定の形式を指定します。 INF の次の例では、文字列と、レジストリにエンドポイント効果の APO を読み込みます - レジストリの追加セクションを示します。

```inf
[Strings]
PKEY_FX_EndpointEffectClsid = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},7"
...
; Driver developers should replace this CLSIDs with that of their own APO
FX_ENDPOINT_CLSID               = "{00000000-0000-0000-0000-000000000000}"
...
[SWAPAPO.I.Association0.AddReg]
HKR,"FX\\0",%PKEY_FX_EndpointEffectClsid%,,%FX_ENDPOINT_CLSID%
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Media クラス INF の拡張機能](media-class-inf-extensions.md)

 

 






