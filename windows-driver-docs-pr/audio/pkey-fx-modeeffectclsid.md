---
title: 鍵\_FX\_ModeEffectClsid
description: Windows 8.1 以降、鍵で\_FX\_ModeEffectClsid プロパティのキーは、ドライバーでサポートされているモード効果 (MFX) を識別します。 ドライバー開発者は、そのドライバーがサポートするサポートされている処理モードの一覧を指定する必要があります。
ms.assetid: 0B15A817-5F49-45B6-AD82-95738C4FF59C
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9639b437aba328403602ee97f5d8db5fc334296
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332096"
---
# <a name="pkeyfxmodeeffectclsid"></a>鍵\_FX\_ModeEffectClsid


Windows 8.1 以降では、**鍵\_FX\_ModeEffectClsid**プロパティのキーは、ドライバーでサポートされているモード効果 (MFX) を識別します。 ドライバー開発者は、そのドライバーがサポートするサポートされている処理モードの一覧を指定する必要があります。

INF ファイルのプロパティのキーは、効果のプロパティ ストアにエンドポイント APOs の Clsid を設定するオーディオ エンドポイント ビルダーに指示します。 この情報は、どのような効果が適用されて、上位レベル アプリを通知するために使用されるオーディオ、グラフの作成に使用されます。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>サンプルの INF ファイル


INF ファイルでは、そのデバイスの追加レジストリ セクションではモードのオーディオ エフェクトの設定を指定します。 INF の次の例では、文字列とモードの効果の APO をレジストリに読み込まれるレジストリの追加セクションを示します。

```inf
[Strings]
PKEY_FX_ModeEffectClsid     = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},6"
...
; Driver developers should replace this CLSIDs with that of their own APO
FX_MODE_CLSID      = "{00000000-0000-0000-0000-000000000000}"
...
[SWAPAPO.I.Association0.AddReg]
HKR,"FX\\0",%PKEY_FX_ModeEffectClsid%,,%FX_MODE_CLSID%
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Media クラス INF の拡張機能](media-class-inf-extensions.md)

 

 






