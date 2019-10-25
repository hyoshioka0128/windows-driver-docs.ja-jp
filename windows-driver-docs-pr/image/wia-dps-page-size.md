---
title: WIA\_DPS\_ページ\_サイズ
description: WIA の\_DPS\_ページ\_SIZE プロパティには、スキャン対象として現在選択されているページのサイズが含まれます。
ms.assetid: 16e32b83-26b8-4283-a937-9fbbe77b42b8
keywords:
- WIA_DPS_PAGE_SIZE イメージングデバイス
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
ms.openlocfilehash: d993a8a2c32659d715aeb61cd944d3791ede2f41
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840716"
---
# <a name="wia_dps_page_size"></a>WIA\_DPS\_ページ\_サイズ


WIA の\_DPS\_ページ\_SIZE プロパティには、スキャン対象として現在選択されているページのサイズが含まれます。

## <span id="ddk_wia_dps_page_size_si"></span><span id="DDK_WIA_DPS_PAGE_SIZE_SI"></span>


プロパティの型: VT\_I4

有効な値: WIA\_PROP\_LIST

アクセス権: 読み取り/書き込み

<a name="remarks"></a>注釈
-------

スキャンするページのサイズを選択するために、アプリケーションでは、WIA\_DPS\_ページ\_サイズに設定します。 このプロパティは、WIA ミニドライバーによって作成および管理されます。

次の表では、 [**WIA\_ip\_ページ\_サイズ**](wia-ips-page-size.md)で有効な定数について説明します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Value</th>
<th>定義</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WIA_PAGE_A4</p></td>
<td><p>ページサイズは8267× 11692 (縦向き) です。</p></td>
</tr>
<tr class="even">
<td><p>WIA_PAGE_CUSTOM</p></td>
<td><p>ページサイズは、 <a href="wia-dps-page-height.md" data-raw-source="[&lt;strong&gt;WIA_DPS_PAGE_HEIGHT&lt;/strong&gt;](wia-dps-page-height.md)"><strong>WIA_DPS_PAGE_HEIGHT</strong></a>プロパティと<a href="wia-dps-page-width.md" data-raw-source="[&lt;strong&gt;WIA_DPS_PAGE_WIDTH&lt;/strong&gt;](wia-dps-page-width.md)"><strong>WIA_DPS_PAGE_WIDTH</strong></a>プロパティの値によって定義されます。</p></td>
</tr>
<tr class="odd">
<td><p>WIA_PAGE_LETTER</p></td>
<td><p>ページサイズは8500× 11000 (縦向き) です。</p></td>
</tr>
</tbody>
</table>

 

[ [**WIA\_ip\_の向き**](wia-ips-orientation.md)] プロパティの値によって、現在選択されているページの向きが決まります。 WIA\_DPS\_ページ\_WIDTH および WIA\_DPS\_PAGE\_HEIGHT プロパティは、ページのディメンション (約1000インチ (001)) を報告します。 これらのプロパティには、ページのディメンションをピクセル単位で含む、 [**wia\_ips\_xextent**](wia-ips-xextent.md)および[**wia\_IP\_yextent**](wia-ips-yextent.md)プロパティと同等の値が必要です。

WIA\_PROP\_リスト型の値は、WIA\_IPS\_ORIENTATION プロパティの有効な設定に依存している必要があります。 Wia\_ページ\_A4 を使用している横向きのドキュメント\_\_をデバイスでスキャンできない場合、wia では、wia の有効な値の一覧には、wia\_DPS\_PAGE\_SIZE プロパティの値が表示されません。\_IP\_方向は LANSCAPE に設定されています。

アプリケーションで、wia\_DPS\_ページの\_サイズを WIA\_PAGE\_CUSTOM 以外の値に設定した場合、ミニドライバーは、WIA\_DPS\_ページ\_WIDTH および WIA の値を調整する必要があり\_DPS\_ページの高さをページのサイズに\_します (1/1000)。 また、ミニドライバーでは、WIA\_IP\_XEXTENT と WIA\_\_IP の値をページのサイズ (ピクセル単位) に調整する必要があります。

エクステント設定 (WIA\_IP\_XEXTENT または WIA\_IP\_YEXTENT) が、現在のページサイズ設定と一致し*ない*値に変更された場合、ミニドライバーは、WIA\_DPS\_ページの値を変更する必要があり\_SIZE プロパティを WIA\_ページ\_カスタムに設定します。 また、ミニドライバーは、新しいエクステントの設定に従って、\_WIDTH または WIA\_DPS\_ページの高さを変更するために\_ページの\_を変更する必要があります。

WIA\_IP\_の方向が LANSCAPE に設定されている場合、エクステントの設定は "反転" されます。 たとえば、アプリケーションで、WIA\_DPS\_ページの\_サイズを WIA\_ページ\_A4 に設定した場合、ミニドライバーでは、WIA\_DPS\_ページ\_幅を11692および WIA\_DPS に設定する必要があり\_ページの高さを8267に\_します。 (ミニドライバーでは、必要に応じて、\_XEXTENT と WIA\_\_IP の\_も WIA を設定する必要があります)。WIA\_DPS\_ページ\_サイズが WIA\_PAGE\_CUSTOM に設定されている場合は、[向き] 設定を使用して、スキャンするページのエクステントサイズを決定することはできません。

ミニドライバーは、WIA\_IP\_の向きプロパティが現在の選択領域と一致していることを確認する必要があります。 アプリケーションで、WIA の\_IP\_方向の値が、現在選択されているページサイズに対して無効なものに変更された場合、ミニドライバーは、\_\_\_WIA の値を変更する必要があります。新しい方向の値。

アプリケーションで、WIA\_DPS\_ページの\_サイズ プロパティを WIA\_ ページに設定している場合\_カスタム を選択した場合、現在の選択領域は影響を受けません。 WIA ミニドライバーは、現在のイメージのレイアウトを取得する必要があります。これは、 [**wia\_ips\_XPOS**](wia-ips-xpos.md)および[**wia\_ip\_YPOS**](wia-ips-ypos.md)プロパティの現在の設定から開始します。 ページサイズの設定によって、スキャナーのベッドの外にある選択領域が表示される場合、ミニドライバーは、WIA\_IPS\_XPOS および WIA\_IP\_YPOS プロパティの値を有効な設定に自動的に調整する必要があります。 WIA\_DPS\_ページ\_SIZE と WIA\_IP\_方向のプロパティが同時に設定され、それらが組み合わせて適用される場合は無効になるため、ミニドライバーは、[**IWiaMiniDrv::D rvvalidateitemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)メソッドでエラーが発生しています。

次の4つのコード例は、次の WIA\_DPS\_ページ\_サイズのシナリオを示しています。

1.  ドライバーは設定を報告します。

2.  アプリケーションは、WIA の\_DPS\_ページの\_SIZE プロパティを WIA\_ページの\_文字に設定します。

3.  アプリケーションでは、 [**WIA\_IPS\_ORIENTATION**](wia-ips-orientation.md)プロパティを LANSCAPE に設定します。

4.  アプリケーションは、 [**WIA\_ip\_XEXTENT**](wia-ips-xextent.md)プロパティを小さい値に変更します。

**例 1: ミニドライバーが設定を報告する**

次のコード例では、アプリケーションが WIA プロパティを設定する前に、ミニドライバーによってカスタムの選択領域が設定されます。 この場合、選択領域は、フラットベッド全体を表します。

WIA_DPS_PAGE_SIZE = WIA_PAGE_CUSTOM WIA_DPS_PAGE_WIDTH = 11500 WIA_DPS_PAGE_HEIGHT = 14000 WIA_IPS_ORIENTATION = 縦長 WIA_IPS_XPOS = 0 WIA_IPS_YPOS = 0 WIA_IPS_XEXTENT = 1150 WIA_IPS_YEXTENT = 1400 WIA_IPS_XRES = 100 WIA_IPS_YRES = 100

**例 2: アプリケーションは、WIA\_DPS\_ページの\_SIZE プロパティを WIA\_ページの\_文字に設定します。**

WIA_DPS_PAGE_SIZE = WIA_PAGE_LETTER WIA_DPS_PAGE_WIDTH = 8500 WIA_DPS_PAGE_HEIGHT = 11000 WIA_IPS_ORIENTATION = 縦長 WIA_IPS_XPOS = 0 WIA_IPS_YPOS = 0 WIA_IPS_XEXTENT = 850 WIA_IPS_YEXTENT = 1100 WIA_IPS_XRES = 100 WIA_IPS_YRES = 100

**例 3: アプリケーションで WIA\_IPS\_ORIENTATION プロパティを LANSCAPE に設定する**

物理的なベッドは、もともと横向きのページを取得できる必要があります。

WIA_DPS_PAGE_SIZE = WIA_PAGE_LETTER WIA_DPS_PAGE_HEIGHT = 11000 WIA_DPS_PAGE_WIDTH = 8500 WIA_IPS_ORIENTATION = LANSCAPE WIA_IPS_XPOS = 0 WIA_IPS_YPOS = 0 WIA_IPS_XEXTENT = 1100 WIA_IPS_YEXTENT = 850 WIA_IPS_XRES = 100 WIA_IPS_YRES = 100

**例 4: アプリケーションが WIA\_IPS\_XEXTENT プロパティを小さい値に変更する**

次のコード例では、アプリケーションによって、WIA\_IPS\_XEXTENT プロパティが1000に変更されます。 ミニドライバーは、wia\_IP\_XEXTENT の新しい値が WIA\_DPS\_PAGE\_SIZE プロパティに対して無効になっていると想定します。これにより、WIA\_DPS\_ページのサイズを変更する必要があります。WIA\_ ページで\_カスタム を設定します。 また、ミニドライバーは、 [**WIA\_DPS\_ページ\_幅**](wia-dps-page-width.md)を調整する必要があります。

WIA_DPS_PAGE_SIZE = WIA_PAGE_CUSTOM WIA_DPS_PAGE_HEIGHT = 1万 WIA_DPS_PAGE_WIDTH = 8500 WIA_IPS_ORIENTATION = LANSCAPE WIA_IPS_XPOS = 0 WIA_IPS_YPOS = 0 WIA_IPS_XEXTENT = 1000 WIA_IPS_YEXTENT = 850 WIA_IPS_XRES = 100 WIA_IPS_YRES = 100

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>バージョン</p></td>
<td><p>Microsoft Windows XP で使用できます。 Windows Vista 以降の場合は、同一の WIA_IPS_PAGE_SIZE プロパティを使用します。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef (Wiadef を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目

[**IWiaMiniDrv::d rvValidateItemProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)

[**WIA\_DPS\_ページ\_の高さ**](wia-dps-page-height.md)

[**WIA\_DPS\_ページ\_サイズ**](wia-dps-page-size.md)

[**WIA\_DPS\_ページ\_幅**](wia-dps-page-width.md)

[**WIA\_IP\_方向**](wia-ips-orientation.md)

[**WIA\_IP\_ページ\_サイズ**](wia-ips-page-size.md)

[**WIA\_IP\_XEXTENT**](wia-ips-xextent.md)

[**WIA\_IP\_XPOS**](wia-ips-xpos.md)

[**WIA\_IP\_YEXTENT**](wia-ips-yextent.md)

[**WIA\_IP\_YPOS**](wia-ips-ypos.md)
