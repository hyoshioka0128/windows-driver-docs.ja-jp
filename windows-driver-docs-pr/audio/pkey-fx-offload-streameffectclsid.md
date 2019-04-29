---
title: 鍵\_FX\_オフロード\_StreamEffectClsid
description: Windows 10 バージョン 1511 以降鍵で\_FX\_オフロード\_StreamEffectClsid プロパティのキーがオフロード再生中に読み込まれるドライバーでサポートされるストリーム効果 (SFX) を識別します。
ms.assetid: 2258E1F8-A96E-4991-B882-00197C2DB0B3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1e736cacd322bd8f26e0c2f81f9d3619af3093d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332098"
---
# <a name="pkeyfxoffloadstreameffectclsid"></a>鍵\_FX\_オフロード\_StreamEffectClsid


Windows 10 バージョン 1511 以降で、**鍵\_FX\_オフロード\_StreamEffectClsid**プロパティ キーは、オフロード中に読み込まれるドライバーでサポートされるストリーム効果 (SFX) を識別します。再生します。 ドライバー開発者は、そのドライバーがピンのオフロードがサポートするストリームがサポートされている効果の一覧を指定する必要があります。

INF ファイルのプロパティのキーは、オフロード用の効果のプロパティ ストアにストリーム効果 APOs の Clsid を設定するオーディオ エンドポイント ビルダーに指示します。 この情報は、どのような効果が適用されて、上位レベル アプリを通知するために使用されるオーディオ、グラフの作成に使用されます。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>サンプルの INF ファイル


INF ファイルでは、そのデバイスの追加レジストリ セクションではモード効果の処理、オーディオの設定を指定します。 文字列とレジストリの追加のセクションではサポートされているストリーミング処理モードをレジストリに読み込まれる INF の次の例を示しています。

```inf
[Strings]
PKEY_FX_Offload_StreamEffectClsid   = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},11"
...
; Driver developers should replace this CLSIDs with that of their own APO
FX_STREAM_CLSID      = "{00000000-0000-0000-0000-000000000000}"
...
[SWAPAPO.AddReg]
HKR,"FX\\0",% PKEY_FX_Offload_StreamEffectClsid %,,%FX_STREAM_CLSID%
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[Media クラス INF の拡張機能](media-class-inf-extensions.md)










