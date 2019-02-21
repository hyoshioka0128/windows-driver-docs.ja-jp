---
title: DCCMD データの読み込み
description: DCCMD データの読み込み
ms.assetid: 2fceaaa6-5604-4130-ae33-8567561fcccb
keywords:
- データ読み込みの WDK DirectX VA をアルファ ブレンド
- ブレンド画像 WDK DirectX va なので、アルファ ブレンドのデータの読み込み
- DCCMD WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb5046a3911ec69a3b954193aaae8332c3beb5cb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56549265"
---
# <a name="loading-dccmd-data"></a>DCCMD データの読み込み


## <span id="ddk_loading_dccmd_data_gg"></span><span id="DDK_LOADING_DCCMD_DATA_GG"></span>


DCCMD (表示コントロール コマンド) のデータは、DVD-ROM 仕様と互換性のある方法で書式設定し、アルファ ブレンド サーフェスを作成する DPXD 画面に強調表示のデータと共に適用されます。 DCCMD データ バッファーの内容は、DVD DCCMDs のリストとして書式設定されたデータので構成されている必要があります。 DVD サブピクチャ定義およびデータ フィールドの解釈の詳細な説明を参照してください。*読み取り専用のディスク、DVD 仕様。パート 3 - ビデオ Specification (version 1.11、1999 年 5 月)* します。

 

 





