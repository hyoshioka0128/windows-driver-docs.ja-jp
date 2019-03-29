---
title: IAMVideoAccelerator API で DXVA およびモーション補正 DDI
description: IAMVideoAccelerator API およびモーション補正 DDI との DirectX VA のリレーションシップ
ms.assetid: 8bfa198f-b29f-491f-8133-a1f3b41e0cbe
keywords:
- DirectX ビデオ アクセラレータ WDK Windows 2000 の表示、IAMVideoAccelerator
- ビデオ アクセラレータ WDK DirectX、IAMVideoAccelerator
- VA WDK DirectX、IAMVideoAccelerator
- IAMVideoAcceleratorNotify
- IAMVideoAccelerator
- ミキシング レンダラー WDK DirectX VA ビデオ
- VMR WDK DirectX VA
- ミキサー WDK DirectX VA をオーバーレイします。
- OVM WDK DirectX VA
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 788b25ccf393d830c439dece55781c819c07f53e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56573652"
---
# <a name="directx-va-relationship-to-iamvideoaccelerator-api-and-motion-compensation-ddi"></a>IAMVideoAccelerator API およびモーション補正 DDI との DirectX VA のリレーションシップ

DirectX VA を使用して、 **IAMVideoAcceleratorNotify**と**IAMVideoAccelerator** (Microsoft Windows SDK に記載されている) インターフェイスと[モーション補正 DDI](motion-compensation.md)ビデオのレンダラー (VMR) またはオーバーレイ ミキサー (OVM) を混在させると、ビデオは、ソフトウェア デコーダー間で交換されるデータの形式を指定するドライバーを表示します。 次の図は、ソフトウェア デコーダー、VMR、ビデオ ディスプレイ ドライバーにこれらのインターフェイスとの関係を示します。

![directx va データ フローを示す図](images/iamvideo.png)

**IAMVideoAcceleratorNotify**インターフェイスを取得または特定のビデオ アクセラレータ GUID の圧縮解除されたバッファー情報を設定します。

**IAMVideoAccelerator**インターフェイスにより、ビデオ アクセラレータの機能にアクセスするためのビデオ デコーダー フィルターとレンダラー (VMR) またはオーバーレイ ミキサー (OVM) を混在させるビデオを使用してビデオのレンダリングを提供します。

DDI 動き補正は、ハードウェア アクセラレーション機能にアクセスでき、ユーザー モード ソフトウェア アプリケーションとの高速化の機能の間、ベンダー間の互換性に共通のインターフェイスを確立します。 DDI ビデオ アクセラレータ オブジェクトが使用されているが開始され、フレーム バッファーのデコードを停止するデコーダーを通知しますハードウェアでサポートされる、画像の圧縮されていない形式を示すし、通知する必要があるマクロ ブロックのディスプレイ ドライバーレンダリングされます。 DDI は動き補正、 [ **DD\_MOTIONCOMPCALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551660)構造体。

詳細については、 **IAMVideoAccelerator**と**IAMVideoAcceleratorNotify**インターフェイス、Windows SDK のドキュメントを参照してください。 DDI 動き補正の詳細については、次を参照してください。[動き補正](motion-compensation.md)と[動き補正コールバック](motion-compensation-callbacks.md)します。

 

 





