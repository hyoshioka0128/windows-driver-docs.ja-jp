---
title: 鍵\_FX\_KeywordDetector\_StreamEffectClsid
description: Windows 10 以降、鍵の\_FX\_KeywordDetector\_StreamEffectClsid プロパティのキーが、キーワードの検出機能のドライバーでサポートされるストリーム効果 (SFX) を識別します。
ms.assetid: C4ED26A0-FDFB-499B-8A61-429E53CCAE6A
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fee9f8ab71264773be7b1a970878db19afdd0d71
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332122"
---
# <a name="pkeyfxkeyworddetectorstreameffectclsid"></a>鍵\_FX\_KeywordDetector\_StreamEffectClsid


Windows 10 以降では、**鍵\_FX\_KeywordDetector\_StreamEffectClsid**プロパティのキーが、キーワードの検出機能のドライバーでサポートされるストリーム効果 (SFX) を識別します。 ドライバー開発者は、キーワード detector の暗証番号 (pin) のドライバーをサポートする効果を 1 つのストリームを指定する必要があります。

INF ファイルのプロパティのキーは、効果のプロパティ ストアにエンドポイント APOs の Clsid を設定するオーディオ エンドポイント ビルダーに指示します。 この情報は、どのような効果が適用されて、上位レベル アプリを通知するために使用されるオーディオ、グラフの作成に使用されます。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>サンプルの INF ファイル


INF ファイルでは、そのデバイスの追加レジストリ セクションでは、エンドポイントのオーディオ デバイスの設定を指定します。 文字列とレジストリを追加のセクションでは、レジストリにキーワード detector ストリーム効果 APO をロードする INF の次の例を示しています。

```inf
[Strings]
PKEY_FX_KeywordDetector_StreamEffectClsid   = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},8"
...
; Driver developers should replace this CLSIDs with that of their own APO
FX_KEYWORD_STREAM_CLSID      = "{00000000-0000-0000-0000-000000000000}"
...
[SWAPAPO.AddReg]
HKR,"FX\\0",%PKEY_FX_KeywordDetector_StreamEffectClsid%,,%FX_KEYWORD_STREAM_CLSID%
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Media クラス INF の拡張機能](media-class-inf-extensions.md)

 

 






