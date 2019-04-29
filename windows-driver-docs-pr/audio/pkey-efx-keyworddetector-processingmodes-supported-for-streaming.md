---
title: 鍵\_EFX\_KeywordDetector\_ProcessingModes\_サポート\_の\_ストリーミング
description: Windows 10 以降、鍵の\_EFX\_KeywordDetector\_ProcessingModes\_サポートされている\_の\_ストリーミング プロパティのキーは、エンド ポイント キーワードの検出機能の処理を識別します。ドライバーでサポートされているストリーミング サポートされているモードです。
ms.assetid: 517B7321-5726-4ADB-9FCD-82776B143FF9
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30079680ad9364c52d3b73013262806bc1cfc532
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332148"
---
# <a name="pkeyefxkeyworddetectorprocessingmodessupportedforstreaming"></a>鍵\_EFX\_KeywordDetector\_ProcessingModes\_サポート\_の\_ストリーミング


Windows 10 以降では、**鍵\_EFX\_KeywordDetector\_ProcessingModes\_サポートされている\_の\_ストリーミング**プロパティのキーを識別します処理モードのドライバーでサポートされているストリーミングのサポート終了点キーワード ディテクターです。 ドライバー開発者には、サポートされているキーワードの detector 暗証番号 (pin)、ドライバーをサポートすることをストリーミング モードの処理の終了点が一覧表示します。

この一覧には、場所、APO 実際にオーディオ信号中に処理するストリーミング シグナル処理モードにはのみが含まれます。 この一覧は、APO 検出目的でのみでサポートされるモードの処理を含めることはできません。

INF ファイルのプロパティのキーには、オーディオ エンドポイント ビルダー APOs の効果のプロパティ ストアに、Clsid を設定するように指示します。 この情報は、どのような効果が適用されて、上位レベル アプリを通知するために使用されるオーディオ、グラフの作成に使用されます。

エンド ポイント効果 (EFX) は、tee 前に、または後、合計であるため処理のエンドポイントに関連付けられている複数のモードは使用できません。 このため、1 つのモードのみオーディオ\_SIGNALPROCESSINGMODE\_既定では、指定することができます。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>サンプルの INF ファイル


INF ファイルでは、そのデバイスの追加レジストリ セクションではモード効果の処理、オーディオの設定を指定します。 文字列とレジストリの追加のセクションでは、ストリーミング処理モードをレジストリにサポートされているキーワードの検出機能を読み込む INF の次の例を示しています。

```inf
[Strings]
PKEY_EFX_KeywordDetector_ProcessingModes_Supported_For_Streaming = "{D3993A3F-99C2-4402-B5EC-A92A0367664B},10"
...
[SWAPAPO.I.Association0.AddReg]
; This line shows how to set the default processing mode for streaming.
HKR,FX\0,%PKEY_EFX_KeywordDetector_ProcessingModes_Supported_For_Streaming%,0x00010000,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Media クラス INF の拡張機能](media-class-inf-extensions.md)

 

 






