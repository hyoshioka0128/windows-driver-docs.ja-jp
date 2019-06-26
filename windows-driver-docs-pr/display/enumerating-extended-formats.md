---
title: 拡張形式の列挙
description: 拡張形式の列挙
ms.assetid: 504464ff-4449-43fa-9fc8-645400ac8236
keywords:
- WDK の DirectX 9.0、拡張の非表示モード
- WDK DirectX 9.0 の非表示モードの拡張
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbbbdd464946532ce1ba20ff33f4bb5234fd8f6c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355545"
---
# <a name="enumerating-extended-formats"></a>拡張形式の列挙


## <span id="ddk_enumerating_extended_formats_gg"></span><span id="DDK_ENUMERATING_EXTENDED_FORMATS_GG"></span>


表示モードを DirectX 9.0 をランタイムがこれらを使用して、操作を実行する前に、ドライバーをサポートする拡張の非表示モードを確認する必要があります。 ドライバーがサポートする非表示モードの数を確認するランタイムの送信、 **GetDriverInfo2** 、D3DGDI2 を使用して要求\_型\_GETEXTENDEDMODECOUNT 値。 ドライバーがすべて非表示モードをサポートしていない場合に 0 を返します、 **dwModeCount**のメンバー、 [ **DD\_GETEXTENDEDMODECOUNTDATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_dd_getextendedmodecountdata)この要求の構造体。 各サポートされる非表示モードに関する情報を受信するランタイムの送信、 **GetDriverInfo2** 、D3DGDI2 を使用して要求\_型\_GETEXTENDEDMODE 値の各モード。 ドライバーが後で非表示モードを指定する D3DDISPLAYMODE 構造体を返す、**モード**のメンバー、 [ **DD\_GETEXTENDEDMODEDATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_dd_getextendedmodedata)構造体。 詳細については**GetDriverInfo2**を参照してください[サポート GetDriverInfo2](supporting-getdriverinfo2.md)します。 D3DDISPLAYMODE の詳細については、DirectX SDK の最新のドキュメントを参照してください。

 

 





