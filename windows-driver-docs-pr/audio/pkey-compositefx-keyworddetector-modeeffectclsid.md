---
title: 鍵\_CompositeFX\_KeywordDetector\_ModeEffectClsid
description: Windows 10 バージョン 1803 以降で、鍵\_CompositeFX\_KeywordDetector\_ModeEffectClsid プロパティのキーは、キーワードの detector 暗証番号 (pin) のドライバーでサポートされているモード効果 (MFX) を識別します。
ms.date: 11/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6d90095ecd9aa410ce625ccc55c5d4a48038234f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556890"
---
# <a name="pkeycompositefxkeyworddetectormodeeffectclsid"></a>鍵\_CompositeFX\_KeywordDetector\_ModeEffectClsid

Windows 10 バージョン 1803 以降では、**鍵\_CompositeFX\_KeywordDetector\_ModeEffectClsid**プロパティ キーは、キーワードのドライバーでサポートされるモードの効果 (MFX) を識別します。検出機能のピン留めします。 ドライバー開発者は、キーワード detector の暗証番号 (pin) のドライバーをサポートする単一のサポートされている処理モードを指定する必要があります。

このプロパティのキーのと同じですが、[鍵\_FX\_KeywordDetector\_ModeEffectClsid](pkey-fx-keyworddetector-modeeffectclsid.md)プロパティのキーが、許可するレジストリの reg 複数文字列として表される複合1 つの位置に複数の効果。

INF ファイルのプロパティのキーは、効果のプロパティ ストアにエンドポイント APOs の Clsid を設定するオーディオ エンドポイント ビルダーに指示します。 この情報は、どのような効果が適用されて、上位レベル アプリを通知するために使用されるオーディオ、グラフの作成に使用されます。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>サンプルの INF ファイル

INF ファイルでは、そのデバイスの追加レジストリ セクションでは、モードのオーディオ効果の設定を指定します。 INF の次の例では、文字列とキーワードの検出機能モード効果 APO をレジストリに読み込まれるレジストリの追加セクションを示します。

```inf
[Strings]
PKEY_CompositeFX_KeywordDetector_ModeEffectClsid     = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},17"
...
; Driver developers should replace this CLSIDs with that of their own APO
SWAP_FX_MODE_CLSID      = "{00000000-0000-0000-0000-000000000000}"
DELAY_FX_STREAM_CLSID   = "{00000000-0000-0000-0000-000000000000}"
...
 
[SWAPAPO.I.Association0.AddReg]
HKR,FX\0,%PKEY_CompositeFX_KeywordDetector_ModeEffectClsid%,0x00010000,%SWAP_FX_MODE_CLSID%,%DELAY_FX_MODE_CLSID%

```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック

[Media クラス INF の拡張機能](media-class-inf-extensions.md)

 

 






