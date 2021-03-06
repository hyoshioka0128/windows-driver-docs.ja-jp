---
title: ウィンドウ表示モードの動作
description: ウィンドウ表示モードの動作
ms.assetid: a852b1d7-5722-4092-a5ff-338dbb2f77b3
keywords:
- ウィンドウ表示モードの回転 WDK の表示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 050bbdaa2458af8760efa5c9764503ae3548e375
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386239"
---
# <a name="windowed-mode-behavior"></a>ウィンドウ表示モードの動作


ウィンドウ表示モードのデバイス用のマイクロソフトの Direct3D ランタイム回転のプライマリ画面に表示するために、回転のプライマリ画面をロックするユーザー モードのディスプレイ ドライバーの関数を呼び出すことはありません。 つまりビット ブロックを実行する回転のプライマリとの間に (bitblt) を転送します。 つまり、ウィンドウ表示モードのデバイスの Direct3D ランタイムは、これらすべての状況を処理します。

ウィンドウ表示モードのデバイスの Direct3D ランタイムには、ユーザー モードのディスプレイ ドライバーの可能性があります呼び出しません[ **OpenResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_openresource)関数およびのユーザー モードのディスプレイ ドライバーを通知するために、共有のプライマリ画面を開きますプライマリのサーフェイスの向き。 ただし、デスクトップ ウィンドウ マネージャー (DWM) が実行されていない場合、Direct3D ランタイムが呼び出す*OpenResource*、ユーザー モードのディスプレイ ドライバーが、プライマリの方向について通知されるとします。 場合にのみ、ドライバーは、独自の目的で (bitblt またはロック) を使ってプライマリ画面にアクセスする必要があります。 に、ユーザー モードのディスプレイ ドライバーがプライマリのサーフェイスの向きの認識にある必要があります。ウィンドウ表示モードのデバイスの Direct3D ランタイムは決して回転したプライマリ画面にアクセスするユーザー モードのディスプレイ ドライバーを要求します。 そのため、ユーザー モードのディスプレイ ドライバーは、独自の内部処理用のプライマリ画面にアクセスする必要がある場合、ドライバーで必要メカニズムへの呼び出しだけでなくその**OpenResource**ために機能*OpenResource*は常に呼び出されません。

DWM またはディスプレイ ミニポート ドライバーの[ **DxgkDdiPresent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dkmddi/nc-d3dkmddi-dxgkddi_present)関数がウィンドウ表示モードのデータを回転します。

 

 





