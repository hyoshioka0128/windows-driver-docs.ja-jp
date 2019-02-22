---
title: ページ サイズと向きのコード例
description: ページ サイズと向きのコード例
ms.assetid: 28425df2-131b-4fbc-ae44-043be2fb4813
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51b1f49c74815c249ef98eed60fa5f2acc325a17
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561113"
---
# <a name="page-size-and-orientation-code-examples"></a>ページ サイズと向きのコード例

これらのコード例は、次の WIA を表示する\_IP\_ページ\_サイズ シナリオ。

1.  ミニドライバーは、設定を報告します。

2.  アプリケーション設定、WIA\_IP\_ページ\_サイズ プロパティは、WIA を\_ページ\_文字。

3.  アプリケーションの設定、 [ **WIA\_IP\_向き**](https://msdn.microsoft.com/library/windows/hardware/ff552625) LANSCAPE するプロパティ。

4.  アプリケーションの変更、 [ **WIA\_IP\_XEXTENT** ](https://msdn.microsoft.com/library/windows/hardware/ff552661)プロパティ値を小さくします。

### <a name="example-1-the-minidriver-reports-the-settings"></a>例 1:設定がレポート、ミニドライバー

次のコード例で、ミニドライバーは、アプリケーション、WIA プロパティを設定する前にカスタム選択領域を設定します。 この場合は、選択範囲は、全体のフラット ベッドを表します。

WIA_IPS_PAGE_SIZE WIA_PAGE_CUSTOM WIA_IPS_PAGE_WIDTH を = = 11500 WIA_IPS_PAGE_HEIGHT 14000 WIA_IPS_ORIENTATION = 縦 WIA_IPS_XPOS を = = 0 WIA_IPS_YPOS = 0 WIA_IPS_XEXTENT 1150 WIA_IPS_YEXTENT = 1400 WIA_IPS_XRES を = = 100 WIA_IPS_YRES = 100

### <a name="example-2-an-application-sets-the-wiaipspagesize-property-to-wiapageletter"></a>例 2:アプリケーション設定、WIA\_IP\_ページ\_サイズ プロパティは、WIA を\_ページ\_文字

次のコード例では、ミニドライバーは、カスタム値から 8500 × 11000 ピクセルの標準のレター サイズにページ サイズを変更します。

WIA_IPS_PAGE_SIZE WIA_PAGE_LETTER WIA_IPS_PAGE_WIDTH を = = 8500 WIA_IPS_PAGE_HEIGHT 11000 WIA_IPS_ORIENTATION = 縦 WIA_IPS_XPOS を = = 0 WIA_IPS_YPOS = 0 WIA_IPS_XEXTENT 850 WIA_IPS_YEXTENT = 1100 WIA_IPS_XRES を = = 100 WIA_IPS_YRES = 100

### <a name="example-3-an-application-sets-the-wiaipsorientation-property-to-lanscape"></a>例 3: アプリケーション設定、WIA\_IP\_LANSCAPE に ORIENTATION プロパティ

次のコード例では、ミニドライバーは、縦から横へページの向きを変更します。 物理ベッドは、当初は横方向にページを取得できる必要があります。

WIA_IPS_PAGE_SIZE WIA_PAGE_LETTER WIA_IPS_PAGE_HEIGHT = 11000 WIA_IPS_PAGE_WIDTH を = = 8500 WIA_IPS_ORIENTATION LANSCAPE WIA_IPS_XPOS を = = 0 WIA_IPS_YPOS = 0 WIA_IPS_XEXTENT = 1100 WIA_IPS_YEXTENT 850 WIA_IPS_XRES を = = 100 WIA_IPS_YRES = 100

### <a name="example-4-an-application-changes-the-wiaipsxextent-property-to-a-smaller-value"></a>例 4:アプリケーションの変更、WIA\_IP\_XEXTENT プロパティ値を小さくする

次のコード例では、アプリケーション変更、 [ **WIA\_IP\_XEXTENT** ](https://msdn.microsoft.com/library/windows/hardware/ff552661) 1000 プロパティ。 ミニドライバーを想定してください WIA に含まれていること、新しい値を\_IP\_XEXTENT が、WIA を無効になった\_IP\_ページ\_SIZE プロパティと、WIA を変更する必要がありますので\_IP\_ページ\_サイズ WIA を\_ページ\_カスタム。 ミニドライバーを調整する必要がありますも[ **WIA\_IP\_ページ\_幅**](https://msdn.microsoft.com/library/windows/hardware/ff552636)します。

WIA_IPS_PAGE_SIZE WIA_PAGE_CUSTOM WIA_IPS_PAGE_HEIGHT を = = 10000 WIA_IPS_PAGE_WIDTH = 8500 WIA_IPS_ORIENTATION LANSCAPE WIA_IPS_XPOS を = = 0 WIA_IPS_YPOS = 0 WIA_IPS_XEXTENT = 1000 WIA_IPS_YEXTENT 850 WIA_IPS_XRES を = = 100 WIA_IPS_YRES = 100
