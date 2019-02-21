---
title: WIA\_DPS\_ページ
description: WIA\_DPS\_自動ドキュメント フィーダーから取得するページの現在の数がページのプロパティに含まれています。
ms.assetid: 51ab2eab-c7b4-4d54-bfc7-d53a8f66c7a9
keywords:
- WIA_DPS_PAGES イメージング デバイス
topic_type:
- apiref
api_name:
- WIA_DPS_PAGES
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f0289268f58ceffcb92c04873d35546fbd3cb4f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56551378"
---
# <a name="wiadpspages"></a>WIA\_DPS\_ページ


WIA\_DPS\_自動ドキュメント フィーダーから取得するページの現在の数がページのプロパティに含まれています。

## <span id="ddk_wia_dps_pages_si"></span><span id="DDK_WIA_DPS_PAGES_SI"></span>


プロパティの種類:VT\_I4

有効な値 :WIA\_PROP\_範囲 (0 から 0 に設定しますスキャナーがスキャンできるページの最大数まで\[0\]を継続的にスキャンします。)。

アクセス権:読み取り/書き込み

<a name="remarks"></a>注釈
-------

アプリケーションの読み取り、WIA\_DPS\_ドキュメント フィーダー付きのページの容量を決定するページのプロパティ。 また、アプリケーションはこのプロパティをスキャンするページの数に設定します。 WIA ミニドライバーを作成し、維持 WIA\_DPS\_ページ。

次の表は、WIA で有効な定数\_DPS\_ページのプロパティ。

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
<td><p>ALL_PAGES</p></td>
<td><p>WIA_PROP_RANGE をゼロ (0) に設定すると同じです。 すべてのページ。 複数のドキュメントではありませんが、ADF に渡すまで継続的にスキャンします。</p></td>
</tr>
</tbody>
</table>

 

**注**  二重モードが有効になっている場合 (つまり、 [ **WIA\_DPS\_ドキュメント\_処理\_選択**](wia-dps-document-handling-select.md)プロパティがフィーダー |双方向)、WIA\_DPS\_ページは依然としてスキャンするページ数。
1 枚の用紙が自動的に入力 2 つのページ二重モードが有効になっている場合、ページの背面にある空白である場合でもです。

WIA を設定した場合\_DPS\_を 1 に、スキャナーのページは、ページの側面の 1 つを処理します。 スキャナーは、二重モードでは、ページの一方だけをスキャンできない場合は、WIA を変更する必要があります\_DPS\_ページ値、 **Inc**のメンバー、 [ **WIA\_プロパティ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff552751)構造体を 2 にします。 この値は、2 つの倍数単位のページを要求する必要がありますが、アプリケーションに通知します。 場合 WIA\_DPS\_ページが 0 は、スキャナーをスキャン*すべて*ドキュメント フィーダーに現在読み込まれているページ。

 

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
<td><p>Microsoft Windows XP で使用できます。 Windows Vista 以降では、同じ WIA_IPS_PAGES プロパティを使用します。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Wiadef.h (Wiadef.h を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目


[**WIA\_DPS\_ドキュメント\_処理\_を選択します**](wia-dps-document-handling-select.md)

[**WIA\_IP\_ページ**](wia-ips-pages.md)

[**WIA\_プロパティ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff552751)

 

 






