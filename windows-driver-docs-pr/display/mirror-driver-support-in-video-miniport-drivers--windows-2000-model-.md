---
title: ビデオのミニポート ドライバー (XDDM) でミラー ドライバーのサポート
description: ビデオ ミニポート ドライバーでのミラー ドライバー サポート (Windows 2000 モデル)
ms.assetid: ca91e0a6-d619-432a-829e-49012951f27c
keywords:
- ビデオのミニポート ドライバー WDK Windows 2000 では、ミラー ドライバー
- ミラー ドライバー WDK Windows 2000 の表示
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: a14f99bcd3e360fe494f27ff2264b3c67d1d205a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358404"
---
# <a name="mirror-driver-support-in-video-miniport-drivers-windows-2000-model"></a>ビデオ ミニポート ドライバーでのミラー ドライバー サポート (Windows 2000 モデル)

*ミラー ドライバー*ミニポート ドライバーには、このようなサポートを試行する特別なコードが持つことはできませんので、Windows 2000 以降、ビデオのミニポート ドライバーが提供されますをサポートします。 参照してください[ミラー ドライバー](mirror-drivers.md)ミラーリング システムでのディスプレイ ドライバーの詳細についてはします。

ミラー ドライバーのミニポート ドライバーの要件はわずかです。 これを実装する必要がありますのみ関数は[ **DriverEntry**](https://msdn.microsoft.com/library/windows/hardware/ff556159)、ミニポート ドライバー、および次によってエクスポートされます。

[*HwVidFindAdapter*](https://msdn.microsoft.com/library/windows/hardware/ff567332)

[*HwVidInitialize*](https://msdn.microsoft.com/library/windows/hardware/ff567345)

[*HwVidStartIO*](https://msdn.microsoft.com/library/windows/hardware/ff567367)

ミラー化されたサーフェイスに関連付けられた物理ディスプレイ デバイスがないため、上記の一覧に表示される関数の 3 つすべてを常に成功を返すための空の実装を使用できます。

**注**  以降 Windows 8 では、ミラー ドライバーがインストールされないシステムにします。 詳細については、次を参照してください。[ミラー ドライバー](mirror-drivers.md)します。

 

 

 





