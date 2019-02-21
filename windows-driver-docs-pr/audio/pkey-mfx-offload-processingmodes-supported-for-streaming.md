---
title: 鍵\_MFX\_オフロード\_ProcessingModes\_サポート\_の\_ストリーミング
description: Windows 10 バージョン 1511 以降鍵で\_MFX\_オフロード\_ProcessingModes\_サポートされている\_の\_ストリーミング プロパティ キーでは、処理モード モード効果を識別します。ドライバーをサポートしてオフロードのストリーミング サポートされています。
ms.assetid: 48E12E69-5159-4483-9891-2B689B7C3DCE
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7db274dbf1490b6b259a22676326bc4a6a3feda2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556889"
---
# <a name="pkeymfxoffloadprocessingmodessupportedforstreaming"></a>鍵\_MFX\_オフロード\_ProcessingModes\_サポート\_の\_ストリーミング


Windows 10 バージョン 1511 以降で、**鍵\_MFX\_オフロード\_ProcessingModes\_サポートされている\_の\_ストリーミング**プロパティのキードライバーをサポートしてオフロードのストリーミング サポートされているモードの処理モードの効果を識別します。 ドライバー開発者には、サポートされている、ドライバーがサポートする、オフロードされたストリーミング モードの処理モードの効果が一覧表示します。

INF ファイルのプロパティのキーには、オーディオ エンドポイント ビルダー APOs の効果のプロパティ ストアに、Clsid を設定するように指示します。 この情報は、どのような効果が適用されて、上位レベル アプリを通知するために使用されるオーディオ、グラフの作成に使用されます。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>サンプルの INF ファイル


INF ファイルでは、そのデバイスの追加レジストリ セクションではモード効果の処理、オーディオの設定を指定します。 文字列とレジストリを追加のセクションでは、レジストリにサポートされている処理モードをストリーミング オフロードをロードする INF の次の例を示しています。

```inf
[Strings]
PKEY_MFX_Offload_ProcessingModes_Supported_For_Streaming = "{D3993A3F-99C2-4402-B5EC-A92A0367664B},12"
...
AUDIO_SIGNALPROCESSINGMODE_DEFAULT = "{C18E2F7E-933D-4965-B7D1-1EEF228D2AF3}"
AUDIO_SIGNALPROCESSINGMODE_MOVIE   = "{B26FEB0D-EC94-477C-9494-D1AB8E753F6E}"
AUDIO_SIGNALPROCESSINGMODE_MEDIA   = "{4780004E-7133-41D8-8C74-660DADD2C0EE}"

...
[SWAPAPO.I.Association0.AddReg]
;To register an APO for streaming in multiple modes, use a REG_MULTI_SZ property and include all the desired modes:
HKR,"FX\\0",%PKEY_MFX_Offload_ProcessingModes_For_Streaming%,%REG_MULTI_SZ%,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%,%AUDIO_SIGNALPROCESSINGMODE_MOVIE%,%AUDIO_SIGNALPROCESSINGMODE_MEDIA%
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Media クラス INF の拡張機能](media-class-inf-extensions.md)

 

 






