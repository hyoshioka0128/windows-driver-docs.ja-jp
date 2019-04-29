---
title: 鍵\_SFX\_KeywordDetector\_ProcessingModes\_サポート\_の\_ストリーミング
description: Windows 10 以降、鍵の\_SFX\_KeywordDetector\_ProcessingModes\_サポートされている\_の\_キーワード detector ストリーミング ストリーミング プロパティのキーを識別しますドライバーでサポートされるモードを処理します。
ms.assetid: E87B3A94-66AF-4557-AB0D-A4D8B0E976E6
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01b1a3bfa2ba6bc628f40aad24b62b035d717773
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332124"
---
# <a name="pkeysfxkeyworddetectorprocessingmodessupportedforstreaming"></a>鍵\_SFX\_KeywordDetector\_ProcessingModes\_サポート\_の\_ストリーミング


Windows 10 以降では、**鍵\_SFX\_KeywordDetector\_ProcessingModes\_サポートされている\_の\_ストリーミング**プロパティのキーを識別しますストリーミング処理モードのドライバーでサポートされているキーワード ディテクターです。 ドライバー開発者には、ストリーミング detector ピンのキーワードのドライバーをサポートしているサポートされている処理モードが一覧表示します。

この一覧には、場所、APO 実際にオーディオ信号中に処理するストリーミング シグナル処理モードにはのみが含まれます。 この一覧は、APO 検出目的でのみでサポートされるモードの処理を含めることはできません。

INF ファイルのプロパティのキーには、オーディオ エンドポイント ビルダー APOs の効果のプロパティ ストアに、Clsid を設定するように指示します。 この情報は、どのような効果が適用されて、上位レベル アプリを通知するために使用されるオーディオ、グラフの作成に使用されます。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>サンプルの INF ファイル


INF ファイルでは、そのデバイスの追加レジストリ セクションではモード効果の処理、オーディオの設定を指定します。 文字列とレジストリを追加のセクションでは、レジストリにキーワード detector pin モードの処理モードの効果をロードする INF の次の例を示しています。

```inf
[Strings]
PKEY_SFX_KeywordDetector_ProcessingModes_Supported_For_Streaming = "{D3993A3F-99C2-4402-B5EC-A92A0367664B},8"
...
AUDIO_SIGNALPROCESSINGMODE_DEFAULT = "{C18E2F7E-933D-4965-B7D1-1EEF228D2AF3}"
AUDIO_SIGNALPROCESSINGMODE_MOVIE   = "{B26FEB0D-EC94-477C-9494-D1AB8E753F6E}"
AUDIO_SIGNALPROCESSINGMODE_COMMUNICATIONS = "{98951333-B9CD-48B1-A0A3-FF40682D73F7}"
...
[SWAPAPO.I.Association0.AddReg]
;To register an APO for streaming in multiple modes, use a REG_MULTI_SZ property and include all the desired modes:
HKR,"FX\\0",%PKEY_SFX_KeywordDetector_ProcessingModes_Supported_For_Streaming%,%REG_MULTI_SZ%,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%,%AUDIO_SIGNALPROCESSINGMODE_MOVIE%,%AUDIO_SIGNALPROCESSINGMODE_COMMUNICATIONS%
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Media クラス INF の拡張機能](media-class-inf-extensions.md)

 

 






