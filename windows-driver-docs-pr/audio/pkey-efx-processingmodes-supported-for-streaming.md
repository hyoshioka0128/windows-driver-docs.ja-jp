---
title: 鍵\_EFX\_ProcessingModes\_サポート\_の\_ストリーミング
description: Windows 8.1 以降、鍵で\_EFX\_ProcessingModes\_サポートされている\_の\_ストリーミング プロパティのキーは、サポートされているドライバーでサポートされているストリーミング モードの処理終了時点を識別します.
ms.assetid: AE905F16-3065-4D7C-A535-143EB77812C9
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a2520efb1a0fd2a62223c29843f364af987f35d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332142"
---
# <a name="pkeyefxprocessingmodessupportedforstreaming"></a>鍵\_EFX\_ProcessingModes\_サポート\_の\_ストリーミング


Windows 8.1 以降では、**鍵\_EFX\_ProcessingModes\_サポートされている\_の\_ストリーミング**プロパティのキーは、処理モードの終了点を識別します。ドライバーでサポートされているストリーミングのサポートされています。 ドライバー開発者が一覧表示、終了ポイントのストリーミング サポートされているモードを処理、ドライバーがサポートします。

INF ファイルのプロパティのキーには、オーディオ エンドポイント ビルダー APOs の効果のプロパティ ストアに、Clsid を設定するように指示します。 この情報は、どのような効果が適用されて、上位レベル アプリを通知するために使用されるオーディオ、グラフの作成に使用されます。

エンド ポイント効果 (EFX) は、tee 前に、または後、合計であるため処理のエンドポイントに関連付けられている複数のモードは使用できません。 このため、1 つのモードのみオーディオ\_SIGNALPROCESSINGMODE\_既定では、指定することができます。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>サンプルの INF ファイル


INF ファイルでは、そのデバイスの追加レジストリ セクションではモード効果の処理、オーディオの設定を指定します。 文字列とレジストリの追加のセクションではサポートされているストリーミング処理モードをレジストリに読み込まれる INF の次の例を示しています。

```inf
[Strings]
PKEY_EFX_ProcessingModes_Supported_For_Streaming = "{D3993A3F-99C2-4402-B5EC-A92A0367664B},7"
...
[SWAPAPO.I.Association0.AddReg]
; This line shows how to set the default processing mode for streaming.
HKR,FX\0,%PKEY_EFX_ProcessingModes_Supported_For_Streaming%,0x00010000,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Media クラス INF の拡張機能](media-class-inf-extensions.md)

 

 






