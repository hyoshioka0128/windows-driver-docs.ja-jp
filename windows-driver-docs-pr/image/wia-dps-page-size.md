---
title: WIA\_DPS\_ページ\_サイズ
description: WIA\_DPS\_ページ\_サイズ プロパティには、スキャンする現在選択されているページのサイズが含まれています。
ms.assetid: 16e32b83-26b8-4283-a937-9fbbe77b42b8
keywords:
- WIA_DPS_PAGE_SIZE イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPS_PAGE_SIZE
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa377ae400a9a5da4a0ba92fe68c4eb649f6848a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571512"
---
# <a name="wiadpspagesize"></a>WIA\_DPS\_ページ\_サイズ


WIA\_DPS\_ページ\_サイズ プロパティには、スキャンする現在選択されているページのサイズが含まれています。

## <span id="ddk_wia_dps_page_size_si"></span><span id="DDK_WIA_DPS_PAGE_SIZE_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_一覧

アクセス権:読み取り/書き込み

<a name="remarks"></a>コメント
-------

アプリケーションをスキャンするページの寸法を選択するには、設定の WIA\_DPS\_ページ\_サイズ。 WIA ミニドライバーは、作成し、このプロパティを保持します。

次の表では有効な定数[ **WIA\_IP\_ページ\_サイズ**](wia-ips-page-size.md)します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>値</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_PAGE_A4</p></td>
<td><p>ページ サイズは、8267 × 11692 (縦向き) です。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PAGE_CUSTOM</p></td>
<td><p>値によって、ページ サイズが定義されている、 <a href="wia-dps-page-height.md" data-raw-source="[&lt;strong&gt;WIA_DPS_PAGE_HEIGHT&lt;/strong&gt;](wia-dps-page-height.md)"> <strong>WIA_DPS_PAGE_HEIGHT</strong> </a>と<a href="wia-dps-page-width.md" data-raw-source="[&lt;strong&gt;WIA_DPS_PAGE_WIDTH&lt;/strong&gt;](wia-dps-page-width.md)"> <strong>WIA_DPS_PAGE_WIDTH</strong> </a>プロパティ。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PAGE_LETTER</p></td>
<td><p>ページ サイズは、8500 × 11000 (縦向き) です。</p></td>
</tr>
</tbody>
</table>

 

値、 [ **WIA\_IP\_向き**](wia-ips-orientation.md)プロパティは、現在選択されているページの向きを決定します。 WIA\_DPS\_ページ\_幅と WIA\_DPS\_ページ\_高さのプロパティ ページのサイズをインチの部分の 1/1000 でのレポート (. 001)。 これらのプロパティの値に相当する必要があります、 [ **WIA\_IP\_XEXTENT** ](wia-ips-xextent.md)と[ **WIA\_IP\_YEXTENT** ](wia-ips-yextent.md)プロパティで、ページの寸法をピクセル単位で含めることができます。

WIA\_PROP\_リストに型指定された値は、WIA の有効な設定に依存する必要があります\_IP\_ORIENTATION プロパティ。 デバイスが、WIA 横向きのドキュメントをスキャンできないかどうか\_ページ\_A4 設定、WIA\_ページ\_A4 が、wia の有効な値の一覧に表示されない\_DPS\_ページ\_SIZE プロパティと WIA\_IP\_LANSCAPE に設定されます。

アプリケーションは、WIA を設定する場合\_DPS\_ページ\_サイズ WIA 以外の値を\_ページ\_カスタム、ミニドライバーは、WIA の値を調整する必要があります\_DPS\_ページ\_幅と WIA\_DPS\_ページ\_インチの部分の 1/1000 のページのサイズの高さ (. 001)。 ミニドライバーは、WIA の値を調整する必要がありますも\_IP\_XEXTENT と WIA\_IP\_YEXTENT をページの寸法をピクセル単位で。

場合、エクステントの設定 (WIA\_IP\_XEXTENT または WIA\_IP\_YEXTENT) が値に変更が*いない*現在のページ サイズ設定と一致、ミニドライバーを変更する必要があります、値、WIA の\_DPS\_ページ\_サイズ プロパティは、WIA を\_ページ\_カスタム。 ミニドライバーは、WIA を変更する必要がありますも\_DPS\_ページ\_幅または WIA\_DPS\_ページ\_新しいエクステント設定に従っての高さ。

場合 WIA\_IP\_LANSCAPE に方向が設定されている、エクステントの設定は「反転します」。 たとえば、アプリケーションは、WIA を設定\_DPS\_ページ\_WIA をサイズ\_ページ\_、A4、ミニドライバーは WIA を設定する必要があります\_DPS\_ページ\_11692 の幅とWIA\_DPS\_ページ\_8267 の高さ。 (、ミニドライバーは、WIA を設定する必要がありますも\_IP\_XEXTENT と WIA\_IP\_YEXTENT 適宜)。その場合に注意してください WIA\_DPS\_ページ\_WIA にサイズが設定されている\_ページ\_カスタム、スキャンするページの範囲の大きさは向きの設定は使用されません。

ミニドライバーことを確認します、WIA\_IP\_選択領域を現在の ORIENTATION プロパティ意見に同意します。 アプリケーションには、WIA の値が変更された場合\_IP\_向きを現在選択されているページ サイズ、ミニドライバーの有効なものは、WIA の値を変更する必要があります\_DPS\_ページ\_ページ サイズ新しい向きの値がサポートされているサイズ。

アプリケーション設定、WIA 場合\_DPS\_ページ\_サイズ プロパティは、WIA を\_ページ\_カスタムでは、現在の選択領域が影響を受けません。 WIA ミニドライバーは、現在のイメージのレイアウトを取得する必要がありますの現在の設定から、 [ **WIA\_IP\_XPOS** ](wia-ips-xpos.md)と[ **WIA\_IP\_YPOS** ](wia-ips-ypos.md)プロパティ。 スキャナーの外にある選択領域の場合、ページ サイズ設定、ミニドライバー、WIA の値に自動的に調整する必要があります\_IP\_XPOS と WIA\_IP\_有効 YPOS プロパティ設定。 場合、WIA\_DPS\_ページ\_サイズと WIA\_IP\_向きプロパティは同時に設定し無効な組み合わせに適用されると、ミニドライバーが失敗する必要があります、アプリケーションの設定でエラーを返すことによって、 [ **IWiaMiniDrv::drvValidateItemProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff545017)メソッド。

次の 4 つのコード例は次の WIA を表示する\_DPS\_ページ\_サイズ シナリオ。

1.  ドライバーは、設定を報告します。

2.  アプリケーション設定、WIA\_DPS\_ページ\_サイズ プロパティは、WIA を\_ページ\_文字。

3.  アプリケーションの設定、 [ **WIA\_IP\_向き**](wia-ips-orientation.md) LANSCAPE するプロパティ。

4.  アプリケーションの変更、 [ **WIA\_IP\_XEXTENT** ](wia-ips-xextent.md)プロパティ値を小さくします。

**例 1:設定がレポート、ミニドライバー**

次のコード例で、ミニドライバーは、アプリケーション、WIA プロパティを設定する前にカスタム選択領域を設定します。 この場合は、選択範囲は、全体のフラット ベッドを表します。

WIA_DPS_PAGE_SIZE WIA_PAGE_CUSTOM WIA_DPS_PAGE_WIDTH を = = 11500 WIA_DPS_PAGE_HEIGHT 14000 WIA_IPS_ORIENTATION = 縦 WIA_IPS_XPOS を = = 0 WIA_IPS_YPOS = 0 WIA_IPS_XEXTENT 1150 WIA_IPS_YEXTENT = 1400 WIA_IPS_XRES を = = 100 WIA_IPS_YRES = 100

**例 2:アプリケーション設定、WIA\_DPS\_ページ\_サイズ プロパティは、WIA を\_ページ\_文字**

WIA_DPS_PAGE_SIZE WIA_PAGE_LETTER WIA_DPS_PAGE_WIDTH を = = 8500 WIA_DPS_PAGE_HEIGHT 11000 WIA_IPS_ORIENTATION = 縦 WIA_IPS_XPOS を = = 0 WIA_IPS_YPOS = 0 WIA_IPS_XEXTENT 850 WIA_IPS_YEXTENT = 1100 WIA_IPS_XRES を = = 100 WIA_IPS_YRES = 100

**例 3:アプリケーション設定、WIA\_IP\_LANSCAPE に ORIENTATION プロパティ**

物理ベッドは、当初は横方向にページを取得できる必要があります。

WIA_DPS_PAGE_SIZE WIA_PAGE_LETTER WIA_DPS_PAGE_HEIGHT = 11000 WIA_DPS_PAGE_WIDTH を = = 8500 WIA_IPS_ORIENTATION LANSCAPE WIA_IPS_XPOS を = = 0 WIA_IPS_YPOS = 0 WIA_IPS_XEXTENT = 1100 WIA_IPS_YEXTENT 850 WIA_IPS_XRES を = = 100 WIA_IPS_YRES = 100

**例 4:アプリケーションの変更、WIA\_IP\_XEXTENT プロパティ値を小さくする**

次のコード例では、アプリケーションを変更、WIA\_IP\_1000 XEXTENT プロパティ。 仮定する必要があります、ミニドライバー WIA の新しい値\_IP\_XEXTENT が、WIA を無効になった\_DPS\_ページ\_SIZE プロパティと、WIA を変更する必要がありますので\_DPS\_ページ\_サイズ WIA を\_ページ\_カスタム。 ミニドライバーを調整する必要がありますも[ **WIA\_DPS\_ページ\_幅**](wia-dps-page-width.md)します。

WIA_DPS_PAGE_SIZE WIA_PAGE_CUSTOM WIA_DPS_PAGE_HEIGHT を = = 10000 WIA_DPS_PAGE_WIDTH = 8500 WIA_IPS_ORIENTATION LANSCAPE WIA_IPS_XPOS を = = 0 WIA_IPS_YPOS = 0 WIA_IPS_XEXTENT = 1000 WIA_IPS_YEXTENT 850 WIA_IPS_XRES を = = 100 WIA_IPS_YRES = 100

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Microsoft Windows XP で使用できます。 Windows Vista 以降では、同じ WIA_IPS_PAGE_SIZE プロパティを使用します。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目

[**IWiaMiniDrv::drvValidateItemProperties**](https://msdn.microsoft.com/library/windows/hardware/ff545017)

[**WIA\_DPS\_ページ\_高さ**](wia-dps-page-height.md)

[**WIA\_DPS\_ページ\_サイズ**](wia-dps-page-size.md)

[**WIA\_DPS\_ページ\_幅**](wia-dps-page-width.md)

[**WIA\_IP\_向き**](wia-ips-orientation.md)

[**WIA\_IP\_ページ\_サイズ**](wia-ips-page-size.md)

[**WIA\_IP\_XEXTENT**](wia-ips-xextent.md)

[**WIA\_IP\_XPOS**](wia-ips-xpos.md)

[**WIA\_IP\_YEXTENT**](wia-ips-yextent.md)

[**WIA\_IP\_YPOS**](wia-ips-ypos.md)
