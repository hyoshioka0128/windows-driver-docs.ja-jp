---
title: 鍵\_CompositeFX\_オフロード\_ModeEffectClsid
description: Windows 10、バージョン 1803 以降鍵で\_CompositeFX\_オフロード\_ModeEffectClsid キーは、オフロード再生中に読み込まれるドライバーでサポートされるモードの効果 (MFX) を識別します。
ms.date: 11/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7e7f6a6d28621051be490bcc9d8068ab3fa21446
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332184"
---
# <a name="pkeycompositefxoffloadmodeeffectclsid"></a>鍵\_CompositeFX\_オフロード\_ModeEffectClsid


Windows 10、バージョン 1803 以降では、**鍵\_CompositeFX\_オフロード\_ModeEffectClsid**キーは、オフロード中に読み込まれるドライバーでサポートされるモードの効果 (MFX) を識別します。再生します。 ドライバー開発者は、そのドライバーがサポートするサポートされている処理モードの一覧を指定する必要があります。

このプロパティのキーのと同じですが、[鍵\_FX\_オフロード\_ModeEffectClsid](pkey-fx-offload-modeeffectclsid.md)プロパティのキーでは複数の効果を許可するレジストリの reg 複数文字列として表現されるコンポジット1 つの位置。

INF ファイルのプロパティのキーには、オーディオ エンドポイント ビルダー モード APOs の効果のプロパティ ストアに、Clsid を設定するように指示します。 この情報は、どのような効果が適用されて、上位レベル アプリを通知するために使用されるオーディオ、グラフの作成に使用されます。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>サンプルの INF ファイル


INF ファイルでは、そのデバイスの追加レジストリ セクションではモード効果の処理、オーディオの設定を指定します。 INF の次の例は、文字列を示し、レジストリの追加のセクションでは、読み込み時に使用されるモードの効果の APO を読み込むには、レジストリに再生をオフロードします。

```inf
[Strings]
PKEY_CompositeFX_Offload_ModeEffectClsid     = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},20"
...
; Driver developers should replace this CLSIDs with that of their own APO
SWAP_FX_MODE_CLSID      = "{00000000-0000-0000-0000-000000000000}"
DELAY_FX_STREAM_CLSID   = "{00000000-0000-0000-0000-000000000000}"
...
 
[SWAPAPO.I.Association0.AddReg]
HKR,FX\0,%PKEY_CompositeFX_Offload_ModeEffectClsid%,0x00010000,%SWAP_FX_MODE_CLSID%,%DELAY_FX_MODE_CLSID%

```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Media クラス INF の拡張機能](media-class-inf-extensions.md)

 

 






