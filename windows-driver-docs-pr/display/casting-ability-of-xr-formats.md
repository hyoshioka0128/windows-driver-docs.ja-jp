---
title: XR 形式のキャスト機能
description: XR 形式のキャスト機能
ms.assetid: 18f9ce6e-df8e-4e57-b86f-338baadcb1b2
keywords:
- Direct3D バージョン 10.1 WDK Windows 7 の表示、XR 形式キャスト機能
- 拡張形式 WDK Windows 7 の表示、XR 形式キャスト機能
- XR 形式キャスト機能 Windows 7 の WDK を表示します。
- Windows 7 の WDK 表示の機能をキャスト
- キャスト機能 Windows 7 の WDK の表示、XR の書式設定します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ad2d04e2631b0ac01b549114a8b57c4b9150cff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572091"
---
# <a name="casting-ability-of-xr-formats"></a>XR 形式のキャスト機能


このセクションでは、Windows 7 およびそれ以降のオペレーティング システムにのみ適用されます。

DXGI\_形式\_R10G10B10\_XR\_バイアス\_A2\_UNORM 形式、DXGI のメンバーである\_形式\_R10G10B10A2\_TYPELESSファミリ。 そのため、アプリケーションは、DXGI をキャストできます\_形式\_R10G10B10\_XR\_バイアス\_A2\_そのファミリの他のメンバーには、「ビュー」の API レベルの概念を通じて UNORM 形式。 この手順は、リソースにアプリケーションを表示する期待される方法です。 具体的には、Direct3D のランタイムのみをスキャンおよびコピー (ドライバーの[ **BltDXGI** ](https://msdn.microsoft.com/library/windows/hardware/ff538252)関数) 形式 XR のリソース\_バイアス。 そのため、リソースをレンダリングするアプリケーション通常のビューを作成 DXGI 形式\_形式\_R10G10B10A2\_UNORM します。

 

 





