---
title: XPSDrv の機能強化
description: このトピックでは、XPSDrv レンダリング アーキテクチャに加えられた更新プログラムに関する情報を提供します。
ms.assetid: 5D76ECA2-C5F6-47E4-BC05-B5137AD4196B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bdc1c53f3a8d5505ecfc23271229e8f6e93c5ce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560352"
---
# <a name="improvements-in-xpsdrv"></a>XPSDrv の機能強化


このトピックでは、XPSDrv レンダリング アーキテクチャに加えられた更新プログラムに関する情報を提供します。

**XPS 形式**

XPS 印刷 API や印刷フィルター パイプラインの間でシームレスに変換されます[Microsoft ホワイト ペーパーの仕様 『 Xml 1.0](https://msdn.microsoft.com/windows/hardware/gg463375) (MS XPS) と[OpenXPS](http://www.ecma-international.org/publications/standards/Ecma-388.htm) (ECMA 388)。 指定しない場合、v4、MS XPS を使用するドライバーの既定を印刷します。 ドライバーは XpsFormat マニフェストのディレクティブを使用して、使用可能な XPS 形式の一方または両方をサポートするために選択できます。 OpenXPS サポートの詳細については、次を参照してください。 [Windows の OpenXPS サポート](https://msdn.microsoft.com/library/windows/hardware/br259130)します。

**XPS ラスタライズ サービスの機能強化**

XPS ラスタライズ サービスが高速の XPS ラスタライズを提供するグラフィックス処理ユニット (GPU) を使用する Windows 8 で改善されました。 これらのパフォーマンスの向上は Windows Display Driver Model (WDDM) 1.2 を使用する gpu を搭載した Windows 8 のシステムで使用できます。 XPS 表示フィルターには、この機能強化を活用するために、変更は不要し、v3 と v4 印刷ドライバーの使用可能なことができます。

XPS ラスタライズ サービスでは、次の精度の高い、新しい形式をなど、いくつかのピクセル形式でラスタライズも提供できます。 その結果、XPS ラスタライズ サービスを使用して印刷ドライバーでは、8 ビット、16 ビットおよび 32 ビット チャネルごとに色の精度が対象ようになりましたことができます。 ピクセル形式の詳細については、次を参照してください。[ネイティブ ピクセル形式の概要](https://msdn.microsoft.com/library/windows/hardware/ee719797.aspx)します。 これらの新しいピクセル形式がサポートされている、 [ **XPSRaterizationFactory1::CreateRasterizer1** ](https://msdn.microsoft.com/library/windows/hardware/hh802468)メソッド。 次の表は、XPS ラスタライズ サービスのピクセル形式を示します。

| Value                                | チャネルの数 | チャネルあたりのビット数 | ピクセルあたりのビット数 | 記憶域の種類 |
|--------------------------------------|---------------|------------------|----------------|--------------|
| GUID\_WICPixelFormat32bppPBGRA       | 4             | 8                | 32             | UINT         |
| GUID\_WICPixelFormat64bppPRGBAHalf   | 4             | 16               | 64             | Float        |
| GUID\_WICPixelFormat128bppPRGBAFloat | 4             | 32               | 128            | Float        |

 

**IPrintCoreHelperUni2**

[IPrintCoreHelperUni2](https://msdn.microsoft.com/library/windows/hardware/hh406580)インターフェイスは GPD ファイルからのコマンド文字列の取得をサポートする Windows 8 で導入されました。 インターフェイスは同じ[IPrintCoreHelperUni](https://msdn.microsoft.com/library/windows/hardware/ff552940)、を除き、追加**GetNamedCommand**メソッド。

## <a name="related-topics"></a>関連トピック
[IPrintCoreHelperUni](https://msdn.microsoft.com/library/windows/hardware/ff552940)  
[IPrintCoreHelperUni2](https://msdn.microsoft.com/library/windows/hardware/hh406580)  
[Microsoft Xml Paper Specification 1.0](https://msdn.microsoft.com/windows/hardware/gg463375)  
[ネイティブのピクセル形式の概要](https://msdn.microsoft.com/library/windows/hardware/ee719797.aspx)  
[OpenXPS](http://www.ecma-international.org/publications/standards/Ecma-388.htm)  
[Windows の OpenXPS サポート](https://msdn.microsoft.com/library/windows/hardware/br259130)  
[V4 プリンター ドライバーのレンダリング アーキテクチャ](v4-driver-rendering-architecture.md)  
[**XPSRaterizationFactory1::CreateRasterizer1**](https://msdn.microsoft.com/library/windows/hardware/hh802468)  



