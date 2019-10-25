---
title: XPSDrv の改善
description: このトピックでは、XPSDrv 表示アーキテクチャに対して行われた更新について説明します。
ms.assetid: 5D76ECA2-C5F6-47E4-BC05-B5137AD4196B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10ff7a5d3cec465f7e850937d20b4aa57940f22a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842310"
---
# <a name="improvements-in-xpsdrv"></a>XPSDrv の改善

このトピックでは、XPSDrv 表示アーキテクチャに対して行われた更新について説明します。

## <a name="xps-format"></a>XPS 形式

XPS 印刷 API や印刷フィルターパイプラインは、 [Microsoft Xml Paper Specification 1.0](https://docs.microsoft.com/en-us/previous-versions/windows/hardware/design/dn614032(v=vs.85)) (MS XPS) と[OpenXPS](http://www.ecma-international.org/publications/standards/Ecma-388.htm) (ECMA-388) の間でシームレスに変換されます。 特に指定がない限り、v4 印刷ドライバーは既定で MS XPS を使用します。 Manifest ディレクティブ XpsFormat を使用すると、ドライバーは、使用可能な XPS 形式のいずれかまたは両方をサポートすることができます。 OpenXPS のサポートの詳細については、「 [OpenXPS support In Windows](https://docs.microsoft.com/windows-hardware/drivers/print/driver-support-for-openxps)」を参照してください。

## <a name="xps-rasterization-service-improvements"></a>XPS ラスタライズサービスの機能強化

XPS ラスタライズサービスが Windows 8 で改良され、グラフィックス処理装置 (GPU) を使用して XPS ラスタライズを高速にするようになりました。 これらのパフォーマンスの向上は、windows Display Driver Model (WDDM) 1.2 を使用する Gpu を搭載した Windows 8 システムで利用できます。 XPS 表示フィルターでは、この改善を利用するための変更は必要ありません。 v3 と v4 の両方の印刷ドライバーで使用できます。

XPS ラスタライズサービスでは、次の新しい高精度形式を含む、いくつかのピクセル形式でラスタライズを行うこともできます。 その結果、XPS ラスタライズサービスを使用する印刷ドライバーは、チャネルあたり8ビット、16ビット、32ビットのカラー精度をターゲットにできるようになりました。 ピクセル形式の詳細については、「[ネイティブピクセル形式の概要](https://docs.microsoft.com/windows/desktop/wic/-wic-codec-native-pixel-formats)」を参照してください。 これらの新しいピクセル形式は、 [**XPSRaterizationFactory1:: CreateRasterizer1**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh802468(v=vs.85))メソッドによってサポートされています。 次の表は、XPS ラスタライズサービスのピクセル形式を示しています。

| Value                                | チャネル数 | チャネルあたりのビット数 | ピクセルあたりのビット数 | 記憶域の種類 |
|--------------------------------------|---------------|------------------|----------------|--------------|
| GUID\_WICPixelFormat32bppPBGRA       | ホーム フォルダーが置かれているコンピューターにアクセスできない             | 8                | 32             | UINT         |
| GUID\_WICPixelFormat64bppPRGBAHalf   | ホーム フォルダーが置かれているコンピューターにアクセスできない             | 16               | 64             | Float        |
| GUID\_WICPixelFormat128bppPRGBAFloat | ホーム フォルダーが置かれているコンピューターにアクセスできない             | 32               | 128            | Float        |

## <a name="iprintcorehelperuni2"></a>IPrintCoreHelperUni2

[IPrintCoreHelperUni2](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni2)インターフェイスは、GPD ファイルからのコマンド文字列の取得をサポートするために Windows 8 で導入されました。 インターフェイスは[Iprintcoreの Peruni](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni)と同じですが、追加の**getnamedcommand**メソッドは除きます。

## <a name="related-topics"></a>関連トピック

[Iprintcoreの Peruni](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni)  

[IPrintCoreHelperUni2](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni2)  

[Microsoft Xml Paper Specification 1.0](https://docs.microsoft.com/en-us/previous-versions/windows/hardware/design/dn614032(v=vs.85))  

[ネイティブピクセル形式の概要](https://docs.microsoft.com/windows/desktop/wic/-wic-codec-native-pixel-formats)  

[OpenXPS](http://www.ecma-international.org/publications/standards/Ecma-388.htm)  

[Windows での OpenXPS のサポート](https://docs.microsoft.com/windows-hardware/drivers/print/driver-support-for-openxps)  

[V4 プリンタードライバーのレンダリングアーキテクチャ](https://docs.microsoft.com/windows-hardware/drivers/print/v4-driver-rendering-architecture)  

[**XPSRaterizationFactory1::CreateRasterizer1**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh802468(v=vs.85))  
