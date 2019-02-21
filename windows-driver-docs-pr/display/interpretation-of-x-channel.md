---
title: チャネル X の解釈
description: チャネル X の解釈
ms.assetid: ba039e5a-78ee-43cb-b883-4675b011a29d
keywords:
- チャネル X、Direct3D バージョン 10.1 WDK Windows 7 の表示
- 拡張形式チャネル X、Windows 7 の WDK の表示
- X チャネル WDK Windows 7 を表示します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: be94ebfc01de84d94cdd28a2f24dfd4297753bcb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558980"
---
# <a name="interpretation-of-x-channel"></a>チャネル X の解釈


このセクションでは、Windows 7 およびそれ以降のオペレーティング システムにのみ適用されます。

ユーザー モードのディスプレイ ドライバーが X を含むすべての形式で X チャネルを読み取る必要があります (たとえば、DXGI\_形式\_B8G8R8X8\_UNORM) としてこのような形式は、ハードウェアや、blender をフィルタ リングに提示されるときに、1.0 f です。

X チャネル コピーする 3-D のパイプラインの外部でデータが移動したときに変更されていない (つまり、アプリケーションを呼び出すと、 **ID3D10Device::CopyResource**、 **ID3D10Device::CopySubresourceRegion**、または**ID3D10Device::UpdateSubResource**メソッド)。 これらのメソッドの詳細については、DirectX SDK のドキュメントを参照してください。

 

 





