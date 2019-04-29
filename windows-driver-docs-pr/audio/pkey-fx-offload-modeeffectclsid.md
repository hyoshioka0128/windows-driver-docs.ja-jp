---
title: 鍵\_FX\_オフロード\_ModeEffectClsid
description: Windows 10 バージョン 1511 以降鍵で\_FX\_オフロード\_ModeEffectClsid キーは、オフロード再生中に読み込まれるドライバーでサポートされるモードの効果 (MFX) を識別します。
ms.assetid: DAA40089-4762-4D26-BEE1-99C1D19783C3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bf468eaff400bfa3657b182ca86a8b14aa7fc36
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332162"
---
# <a name="pkeyfxoffloadmodeeffectclsid"></a>鍵\_FX\_オフロード\_ModeEffectClsid


Windows 10 バージョン 1511 以降で、**鍵\_FX\_オフロード\_ModeEffectClsid**キー オフロード再生中に読み込まれるドライバーでサポートされるモードの効果 (MFX) を識別します。 ドライバー開発者は、そのドライバーがサポートするサポートされている処理モードの一覧を指定する必要があります。

INF ファイルのプロパティのキーには、オーディオ エンドポイント ビルダー モード APOs の効果のプロパティ ストアに、Clsid を設定するように指示します。 この情報は、どのような効果が適用されて、上位レベル アプリを通知するために使用されるオーディオ、グラフの作成に使用されます。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>サンプルの INF ファイル


INF ファイルでは、そのデバイスの追加レジストリ セクションではモード効果の処理、オーディオの設定を指定します。 INF の次の例は、文字列を示し、レジストリの追加のセクションでは、読み込み時に使用されるモードの効果の APO を読み込むには、レジストリに再生をオフロードします。

```inf
[Strings]
PKEY_FX_Offload_ModeEffectClsid     = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},12"
...
; Driver developers should replace this CLSIDs with that of their own APO
FX_MODE_CLSID      = "{00000000-0000-0000-0000-000000000000}"
...
[SWAPAPO.I.Association0.AddReg]
HKR,"FX\\0",%PKEY_FX_Offload_ModeEffectClsid%,,%FX_MODE_CLSID%
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Media クラス INF の拡張機能](media-class-inf-extensions.md)

 

 






