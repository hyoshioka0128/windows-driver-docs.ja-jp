---
title: XR 形式のキャスト機能
description: XR 形式のキャスト機能
ms.assetid: 18f9ce6e-df8e-4e57-b86f-338baadcb1b2
keywords:
- Direct3D バージョン 10.1 WDK Windows 7 display、XR 形式のキャスト機能
- 拡張形式 WDK Windows 7 display、XR format キャスト機能
- XR 形式キャスト機能 WDK Windows 7 ディスプレイ
- 機能を備えた WDK Windows 7 ディスプレイのキャスト
- XR の機能である WDK Windows 7 display、形式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bcc99c2cb7b89bf6984424141122839f0171e4a4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839058"
---
# <a name="casting-ability-of-xr-formats"></a>XR 形式のキャスト機能


このセクションは、Windows 7 以降のオペレーティングシステムにのみ適用されます。

DXGI\_形式\_R10G10B10\_XR\_バイアス\_A2\_UNORM 形式は、R10G10B10A2\_タイプレスファミリの DXGI\_形式のメンバーです。 そのため、アプリケーションは、"views" の API レベルの概念を通じて、そのファミリの他のメンバーに対して、R10G10B10\_XR\_バイアス\_A2\_UNORM 形式\_\_形式をキャストできます。 この手順は、アプリケーションがリソースに対してレンダリングするために必要な方法です。 具体的には、Direct3D ランタイムは、format XR\_BIAS という形式のリソースをスキャンして、(ドライバーの[**Bltdxgi**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxgiddi/ns-dxgiddi-dxgi_ddi_base_functions)関数を通じて) コピーすることしかできません。 そのため、リソースにレンダリングするために、アプリケーションは通常、R10G10B10A2\_UNORM という形式の\_\_形式のビューを作成します。

 

 





