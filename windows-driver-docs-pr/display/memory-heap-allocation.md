---
title: メモリ ヒープの割り当て
description: メモリ ヒープの割り当て
ms.assetid: 669dce85-ed37-4d47-88d6-115cb3a2e419
keywords:
- stride WDK DirectDraw
- ピッチを WDK DirectDraw
- WDK DirectDraw のオフセット
- ヒープ メモリ WDK DirectDraw を描画するには、
- DirectDraw メモリ ヒープ、WDK の Windows 2000 の表示
- WDK DirectDraw、ヒープ メモリ
- ヒープ メモリ WDK の DirectDraw を表示します。
- ヒープ WDK DirectDraw
- ヒープのメモリを割り当てる
- グラフィックスアクセラレータ
- サーフェスの WDK DirectDraw、メモリ ヒープの割り当て
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff22c0efb3a486e0659e3e56466b76a3aa99398e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385609"
---
# <a name="memory-heap-allocation"></a>メモリ ヒープの割り当て


## <span id="ddk_memory_heap_allocation_gg"></span><span id="DDK_MEMORY_HEAP_ALLOCATION_GG"></span>


サーフェスを割り当て、DirectDraw をスキャン表示メモリ ヒープ、ドライバーによって指定された順序で。 ヒープがの配列の指定された[**グラフィックスアクセラレータ**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_videomemory)構造体。 DirectDraw は、グラフィックスアクセラレータ構造体、配列内の順序でヒープを走査します。 グラフィックスアクセラレータ構造体では、ヒープへのアクセスを記述するフラグをヒープの開始と終了のメモリ アドレスなどの特定のメトリックに設定し、使用法の種類は、画面のこのヒープ内に配置の制限されます。 DirectDraw はないときを作成し、各ヒープの管轄下サーフェスの破棄は、メモリの割り当てを解除して、ヒープを管理します。 物理的な制限は、これらの属性を設定する方法を決定します。

DirectDraw のヒープ マネージャーは、2 つのパスを通じて、 [**グラフィックスアクセラレータ**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_videomemory)サーフェスの作成またはリストアへの応答でのメモリを割り当てる際の構造体します。 **DdsCaps**グラフィックスアクセラレータ構造体のメンバーに通知 DirectDraw ヒープ内にどのようなメモリは最初のパスで使用できません。 たとえば、ヒープがちょうどよいバック バッファーの大きさの場合は、スプライトから除外できます、DDSCAPS を設定して、最初のパスに割り当てられている\_OFFSCREENPLAIN フラグ。 これにより、他のヒープでいっぱいにオフスクリーン サーフェスはプレーンなページの反転のバック バッファーを維持しながらします。

**DdsCapsAlt**グラフィックスアクセラレータ構造体のメンバーは、2 番目のパスでスプライトを許可する設定できます。 そうすること場合は、その他のヒープでスプライトを作成できませんでした、問題のヒープでのみ、スプライトを許可できます。 DDSCAPS を指定しない\_OFFSCREENPLAIN フラグ**ddsCapsAlt**します。 これにより、代替の使用を取り除くことがなく、最適に使用するヒープができます。

表示メモリ ヒープ線形または、ブリット機能に応じて、四角形のいずれかまたは既存のニーズのディスプレイ ドライバー。 **DwFlags**のメンバー、 [**グラフィックスアクセラレータ**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_videomemory)構造体を使用して、メモリ割り当ての種類を指定します。 線形のヒープには、各画面のピッチを異なるできるメモリの領域について説明します。 四角形のヒープには、各画面のピッチは固定されているメモリの領域について説明します。 これらのヒープを混合および必要に応じて、同じのディスプレイ カード内で一致することができます。 詳細については、次を参照してください。[メモリ構成](memory-configurations.md)します。

画面のメモリ*ピッチ*、stride または offset とも呼ばれる、次のスキャン ラインの表示メモリの同じ列を達成するために、メモリの表示の列に追加されたバイト数です。 ピッチはピクセル単位ではなくバイト単位、640 x 480 x 8 の画面で同じ幅と高さの寸法が別のピクセル形式 (ビット単位の深さ)、画面よりもさまざまなピッチの値があります。 さらに、ピッチの値には、ランタイムがと共に配置要件のための追加のバイトのキャッシュとして予約されている追加のバイト場合がありますが反映されます。 そのため、想定することはできません、声の高さはピクセルあたりのバイトの数を乗算して、画面の幅だけです。 代わりに、幅と次の図に示すように、ピッチの違いを視覚化します。

![幅とピッチの違いを示す図](images/ddfig3.png)

前述のように、ピッチの値を決定するときにアカウントの配置の要件も考慮する必要があります。 たとえば、ピクセル (bpp) 画面あたり 1 バイトが 97 ピクセルとします。 また、ハードウェアまたはディスプレイ ドライバーが DWORD (4 バイト) の配置が必要であるとします。 場合は、ランタイムはキャッシュのバイト数を予約していない、ピッチは 100、これは 97 以上大きい番号の [次へ] が 4 で均等に割り切れるです。 次の計算は、このピッチの値を決定します。

```cpp
pitch = bpp * width + ( 4 - ( bpp * width) % 4 )
// that is, pitch = 97 + (4 - 1) = 100
```

 

 





