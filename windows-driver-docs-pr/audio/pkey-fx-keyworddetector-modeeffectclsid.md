---
title: 鍵\_FX\_KeywordDetector\_ModeEffectClsid
description: Windows 10 以降、鍵の\_FX\_KeywordDetector\_ModeEffectClsid プロパティのキーは、キーワードの detector 暗証番号 (pin) のドライバーでサポートされているモード効果 (MFX) を識別します。
ms.assetid: 67030999-0658-4880-9CC8-A25496DE584E
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce7adbf5a9ccd819806f80ae19ef7d6b70e18be7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332134"
---
# <a name="pkeyfxkeyworddetectormodeeffectclsid"></a>鍵\_FX\_KeywordDetector\_ModeEffectClsid


Windows 10 以降では、**鍵\_FX\_KeywordDetector\_ModeEffectClsid**プロパティのキーは、キーワードの detector 暗証番号 (pin) のドライバーでサポートされているモード効果 (MFX) を識別します。 ドライバー開発者は、キーワード detector の暗証番号 (pin) のドライバーをサポートする単一のサポートされている処理モードを指定する必要があります。

INF ファイルのプロパティのキーは、効果のプロパティ ストアにエンドポイント APOs の Clsid を設定するオーディオ エンドポイント ビルダーに指示します。 この情報は、どのような効果が適用されて、上位レベル アプリを通知するために使用されるオーディオ、グラフの作成に使用されます。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>サンプルの INF ファイル


INF ファイルでは、そのデバイスの追加レジストリ セクションではモードのオーディオ エフェクトの設定を指定します。 INF の次の例では、文字列とキーワードの検出機能モード効果の APO をレジストリに読み込まれるレジストリの追加セクションを示します。

```inf
[Strings]
PKEY_FX_KeywordDetector_ModeEffectClsid     = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},9"
...
; Driver developers should replace this CLSIDs with that of their own APO
FX_KEYWORD_MODE_CLSID      = "{00000000-0000-0000-0000-000000000000}"
...
[SWAPAPO.I.Association0.AddReg]
HKR,"FX\\0",%PKEY_FX_KeywordDetector_ModeEffectClsid%,,%FX_KEYWORD_MODE_CLSID%
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Media クラス INF の拡張機能](media-class-inf-extensions.md)

 

 






