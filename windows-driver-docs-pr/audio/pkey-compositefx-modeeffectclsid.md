---
title: 鍵\_CompositeFX\_ModeEffectClsid
description: Windows 10 バージョン 1803 の後で、鍵\_Compositefx\_ModeEffectClsid プロパティのキーは、ドライバーでサポートされているモード効果 (MFX) を識別します。 ドライバー開発者は、そのドライバーがサポートするサポートされている処理モードの一覧を指定する必要があります。
ms.date: 11/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4b8f84e6d73c02b86aeb808b60a292a79b8179c8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56557121"
---
# <a name="pkeycompositefxmodeeffectclsid"></a>鍵\_CompositeFX\_ModeEffectClsid

Windows 10 バージョン 1803 以降では、**鍵\_CompositeFX\_ModeEffectClsid**プロパティのキーは、ドライバーでサポートされているモード効果 (MFX) を識別します。 ドライバー開発者は、そのドライバーがサポートするサポートされている処理モードの一覧を指定する必要があります。

このプロパティのキーのと同じですが、[鍵\_FX\_ModeEffectClsid](pkey-fx-modeeffectclsid.md)プロパティのキーでは 1 つの位置に複数の効果を許可するレジストリの reg 複数文字列として表現されるコンポジット。

INF ファイルのプロパティのキーは、効果のプロパティ ストアにエンドポイント APOs の Clsid を設定するオーディオ エンドポイント ビルダーに指示します。 この情報は、どのような効果が適用されて、上位レベル アプリを通知するために使用されるオーディオ、グラフの作成に使用されます。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>サンプルの INF ファイル

INF ファイルでは、そのデバイスの追加レジストリ セクションではモードのオーディオ エフェクトの設定を指定します。 INF の次の例では、文字列とモードの効果の APO をレジストリに読み込まれるレジストリの追加セクションを示します。

```inf
[Strings]
PKEY_CompositeFX_ModeEffectClsid     = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},14"
...
; Driver developers should replace this CLSIDs with that of their own APO
SWAP_FX_MODE_CLSID      = "{00000000-0000-0000-0000-000000000000}"
DELAY_FX_STREAM_CLSID   = "{00000000-0000-0000-0000-000000000000}"
...
 
[SWAPAPO.I.Association0.AddReg]
HKR,FX\0,%PKEY_CompositeFX_ModeEffectClsid%,0x00010000,%SWAP_FX_MODE_CLSID%,%DELAY_FX_MODE_CLSID%

```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Media クラス INF の拡張機能](media-class-inf-extensions.md)

 

 






