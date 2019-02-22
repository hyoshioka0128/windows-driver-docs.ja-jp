---
title: ヒープの拡張の制限
description: ヒープの拡張の制限
ms.assetid: 4f907768-670a-4ce5-b2d7-7af27baf80da
keywords:
- 拡張セキュリティ機能 WDK DirectDraw を描画するには、ヒープします。
- DirectDraw 機能を拡張しサーフェス WDK Windows 2000 の表示、ヒープ
- WDK DirectDraw、ヒープ拡張セキュリティ機能
- ヒープ WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2d9ef2a829691e0412b581c134c966527e1e149
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527442"
---
# <a name="extended-heap-restrictions"></a>ヒープの拡張の制限


## <span id="ddk_extended_heap_restrictions_gg"></span><span id="DDK_EXTENDED_HEAP_RESTRICTIONS_GG"></span>


[ **DD\_MORESURFACECAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff551659)構造体が変数のサイズ。 常に、 **ddsCapsMore** 、メンバーは、0 個以上必要があります**ddsExtendedHeapRestrictions**エントリ。 ドライバーにある GUID に応答した場合、\_DDMoreSurfaceCaps クエリでは、その DD を返す必要があります\_MORESURFACECAPS 構造を多く含む**ddsExtendedHeapRestrictions**ほどエントリに返される表示メモリヒープで、 [ **DD\_HALINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551627)構造 (DirectDraw を保証する GUID\_ドライバー レポート DD後DDMoreSurfaceCapsクエリが行われた\_HALINFO)。

ドライバーは、適切な入力する必要がありますも**dwSize** 、DD の値\_MORESURFACECAPS 構造体。 値**dwSize**はこの方法で計算されます。

```cpp
DDMORESURFACECAPS.dwSize = 
          (DWORD) (sizeof(DDMORESURFACECAPS) 
        + (((signed int)DDHALINFO.vmiData.dwNumHeaps) - 1) 
        * sizeof(DDSCAPSEX)*2 );
```

値から 1 を引いてことに注意してください**dwNumHeaps**という事実を考慮する必要です、 [ **DD\_MORESURFACECAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff551659)構造体には、 **ddsExtendedHeapRestrictions**メンバー 1 つの要素の配列であります。 だけで、最初より後の要素を配列もの (つまりから<strong>ddsExtendedHeapRestrictions\[</strong>1<strong>\]</strong>で) DDの合計サイズの計算にカウントする必要があります\_MORESURFACECAPS 構造体。

**DdsCapsEx**と**ddsCapsExAlt**メンバーと同様に、 **ddsCaps**と**ddsCapsAlt** の配列のメンバー[**グラフィックスアクセラレータ**](https://msdn.microsoft.com/library/windows/hardware/ff570171)で返される構造体、 **pvmList**のメンバー、 [ **VIDEOMEMORYINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff570172)構造体のメンバーとして含まれている、 [ **DD\_HALINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551627)構造体。 設定いずれかのビット**ddsCapsEx**ビット セットがそのヒープで配置されていない必要がありますで表示されることを意味します。 設定いずれかのビット、 **ddsCapsExAlt**メンバーは、画面は、そのヒープ内に配置することはできないことを意味します。 サーフェス、DirectDraw を最初に割り当てて、すべてのヒープを通過するときとないする機能ビットのヒープが見つかった場合は、 **ddsCaps**サーフェスの DDSCAPS ビット グラフィックスアクセラレータ構造体の一致のメンバーは、割り当て、そのヒープ内のサーフェイス。 このパスには、このようなヒープでは、検出されないかどうかは、DirectDraw により、同じパスのチェックが、 **ddsCapsEx**フィールド。 このパスは、任意のヒープを検索する失敗した場合、サーフェスは、ヒープで作成できません。

 

 





