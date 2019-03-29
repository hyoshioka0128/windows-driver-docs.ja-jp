---
title: 鍵\_SFX\_オフロード\_ProcessingModes\_サポート\_の\_ストリーミング
description: Windows 10 バージョン 1511 以降鍵で\_SFX\_オフロード\_ProcessingModes\_サポートされている\_の\_ストリーミング プロパティのキーは、ストリーミング処理のオフロードを識別します。ドライバーでサポートされるモード。
ms.assetid: 063F75D6-AA00-4096-8CFC-633A51648333
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4de8ba0947c2937b99e5212ffbdd3c9a671ad5b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581661"
---
# <a name="pkeysfxoffloadprocessingmodessupportedforstreaming"></a>鍵\_SFX\_オフロード\_ProcessingModes\_サポート\_の\_ストリーミング


Windows 10 バージョン 1511 以降で、**鍵\_SFX\_オフロード\_ProcessingModes\_サポートされている\_の\_ストリーミング**プロパティのキーストリーミング処理モードのドライバーをサポートしてオフロードを識別します。 ドライバー開発者には、そのドライバーがピンのオフロードがサポートする、オフロードされたストリーミング サポートされている処理モードが一覧表示します。

この一覧には、場所、APO 実際にオーディオ信号の間に処理オフロード ストリーミング シグナル処理モードにはのみが含まれます。 この一覧は、APO 検出目的でのみでサポートされるモードの処理を含めることはできません。

INF ファイルのプロパティのキーは、効果のプロパティ ストアにオフロード APOs の Clsid を設定するオーディオ エンドポイント ビルダーに指示します。 この情報は、どのような効果が適用されて、上位レベル アプリを通知するために使用されるオーディオ、グラフの作成に使用されます。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>サンプルの INF ファイル


INF ファイルでは、そのデバイスの追加レジストリ セクションではモード効果の処理、オーディオの設定を指定します。 文字列とレジストリを追加のセクションでは、ストリーミング処理モードをレジストリにオフロードの暗証番号 (pin) のサポートをロードする INF の次の例を示しています。

```inf
[Strings]
PKEY_SFX_Offload_ProcessingModes_Supported_For_Streaming = "{D3993A3F-99C2-4402-B5EC-A92A0367664B},11"
...
AUDIO_SIGNALPROCESSINGMODE_DEFAULT = "{C18E2F7E-933D-4965-B7D1-1EEF228D2AF3}"
AUDIO_SIGNALPROCESSINGMODE_MOVIE   = "{B26FEB0D-EC94-477C-9494-D1AB8E753F6E}"
AUDIO_SIGNALPROCESSINGMODE_MEDIA   = "{4780004E-7133-41D8-8C74-660DADD2C0EE}"
...
[SWAPAPO.I.Association0.AddReg]
;To register an APO for offload streaming in multiple modes, use a REG_MULTI_SZ property and include all the desired modes:
HKR,"FX\\0",%PKEY_SFX_Offload_ProcessingModes_Supported_For_Streaming%,%REG_MULTI_SZ%,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%,%AUDIO_SIGNALPROCESSINGMODE_MOVIE%,%AUDIO_SIGNALPROCESSINGMODE_MEDIA%
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Media クラス INF の拡張機能](media-class-inf-extensions.md)

 

 






