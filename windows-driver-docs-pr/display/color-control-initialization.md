---
title: カラー コントロールの初期化
description: カラー コントロールの初期化
ms.assetid: dd3afcaa-3da0-4515-8b8d-e7429792be23
keywords:
- WDK DirectDraw、コントロールの初期化の色の描画
- DirectDraw WDK Windows 2000 の表示、カラー コントロールの初期化
- コントロールの初期化 WDK DirectDraw を色します。
- DirectDraw カラー コントロールの初期化
- DdControlColor
- 輝度 WDK DirectDraw
- WDK DirectDraw の明るさ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b87f8af3137ba97a96f2d95cbb8d08e978b0003
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354235"
---
# <a name="color-control-initialization"></a>カラー コントロールの初期化


## <span id="ddk_color_control_initialization_gg"></span><span id="DDK_COLOR_CONTROL_INITIALIZATION_GG"></span>


ドライバーの[ *DdControlColor* ](https://msdn.microsoft.com/library/windows/hardware/ff549244)関数は、オーバーレイやプライマリ画面の輝度/明るさコントロールを制御します。 色の管理機能を有効にするには、Microsoft DirectDraw HAL は初期化時に、次を行う必要があります。

-   オーバーレイやプライマリ サーフェスにカラー コントロールが含まれる場合の設定、DDCAPS2\_COLORCONTROLOVERLAY や DDCAPS2\_COLORCONTROLPRIMAY でフラグを設定、 **dwCaps2**のメンバー、 [ **DDCORECAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549248)構造体に埋め込まれている、 [ **DD\_HALINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551627)構造体。

-   ドライバーは、DD で関数を指定する必要があります\_HALINFO 構造 DirectDraw 呼び出すことができる追加情報を取得します。 「 [ **DdGetDriverInfo**](https://msdn.microsoft.com/library/windows/hardware/ff549404)します。

-   [ **DdGetDriverInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff549404)の GUID を持つコールバックを呼び出す必要があります\_ColorControlCallbacks GUID を指定します。 ドライバーを入力する必要があります、 [ **DD\_COLORCONTROLCALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff550521)適切なドライバーのコールバックとフラグが設定された構造化し、この構造のコピー、 **lpvData**入力構造体のメンバー。

 

 





