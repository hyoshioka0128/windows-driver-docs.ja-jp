---
title: ウィンドウ表示モードの動作
description: ウィンドウ表示モードの動作
ms.assetid: a852b1d7-5722-4092-a5ff-338dbb2f77b3
keywords:
- 'ウィンドウモードのローテーション: WDK ディスプレイ'
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 018d8f85bbf6eb091232c5aa7f04be0c3b3cbb27
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829143"
---
# <a name="windowed-mode-behavior"></a>ウィンドウ表示モードの動作


ウィンドウモードのデバイス用の Microsoft Direct3D ランタイムは、回転したプライマリサーフェイスをロックしたり、回転したプライマリサーフェイスにレンダリングしたり、回転したプライマリとの間でビットブロック転送 (bitblt) を実行したりするために、ユーザーモードのディスプレイドライバーの機能を呼び出すことはありません。 つまり、ウィンドウモードのデバイス用の Direct3D ランタイムは、このような状況をすべて処理します。

ウィンドウモードのデバイス用の Direct3D ランタイムでは、ユーザーモードの表示ドライバーの[**Openresource**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_openresource)関数を呼び出して、共有プライマリサーフェイスを開き、プライマリサーフェイスの向きをユーザーモード表示ドライバーに通知することはできません。 ただし、デスクトップウィンドウマネージャー (DWM) が実行されていない場合、Direct3D ランタイムは*Openresource*を呼び出し、ユーザーモードの表示ドライバーはプライマリの向きについて通知されます。 ユーザーモードの表示ドライバーは、ドライバーが (bitblt またはロックを使用して) 独自の目的でプライマリサーフェイスにアクセスする必要がある場合にのみ、主な表面の向きを認識している必要があります。ウィンドウモードのデバイス用の Direct3D ランタイムは、回転したプライマリ画面にアクセスするためにユーザーモードのディスプレイドライバーを要求することはありません。 したがって、ユーザーモード表示ドライバーが独自の内部目的でプライマリサーフェイスにアクセスする必要がある場合、 *openresource*は常に呼び出されないため、ドライバーには**openresource**関数の呼び出しに加えて、機構が必要です。

DWM または display ミニポートドライバーの[**DxgkDdiPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_present)関数は、ウィンドウモードのデータを回転します。

 

 





