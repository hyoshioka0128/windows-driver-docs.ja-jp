---
title: 拡張形式の列挙
description: 拡張形式の列挙
ms.assetid: 504464ff-4449-43fa-9fc8-645400ac8236
keywords:
- 非標準の表示モード WDK DirectX 9.0、拡張
- 拡張非標準表示モード (WDK DirectX 9.0)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d24793d2ca3d130533515d2dabe52956422bf03a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839697"
---
# <a name="enumerating-extended-formats"></a>拡張形式の列挙


## <span id="ddk_enumerating_extended_formats_gg"></span><span id="DDK_ENUMERATING_EXTENDED_FORMATS_GG"></span>


DirectX 9.0 ランタイムは、これらの表示モードを使用して操作を実行する前に、ドライバーがサポートする拡張非標準表示モードを確認する必要があります。 ドライバーがサポートしている非標準の表示モードの数を確認するために、ランタイムは D3DGDI2\_TYPE\_GETEXTENDEDMODECOUNT value を使用して**GetDriverInfo2**要求を送信します。 ドライバーが非標準の表示モードをサポートしていない場合は、この要求の[**DD\_GETEXTENDEDMODECOUNTDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_getextendedmodecountdata)構造体の**dwModeCount**メンバーで0が返されます。 サポートされている非標準表示モードに関する情報を受信するために、ランタイムは、各モードの D3DGDI2\_TYPE\_GETEXTENDEDMODE 値を使用して**GetDriverInfo2**要求を送信します。 次に、このドライバーは、 [**DD\_GETEXTENDEDMODEDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_dd_getextendedmodedata)構造体の**mode**メンバーで非標準の表示モードを指定する D3DDISPLAYMODE 構造体を返します。 **GetDriverInfo2**の詳細については、「 [GetDriverInfo2 のサポート](supporting-getdriverinfo2.md)」を参照してください。 D3DDISPLAYMODE の詳細については、最新の DirectX SDK のドキュメントを参照してください。

 

 





