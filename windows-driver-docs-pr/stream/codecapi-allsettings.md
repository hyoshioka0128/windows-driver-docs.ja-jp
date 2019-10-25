---
title: CODECAPI\_ALLSETTINGS
description: CODECAPI\_ALLSETTINGS
ms.assetid: 0ae11200-af21-476a-89a8-515bd98920a0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31d92b135efd6bfbfddd3446d06c159643d75c92
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844732"
---
# <a name="codecapi_allsettings"></a>CODECAPI\_ALLSETTINGS


## <span id="ddk_codecapi_allsettings_ks"></span><span id="DDK_CODECAPI_ALLSETTINGS_KS"></span>


CODECAPI\_ALLSETTINGS プロパティは、ミニドライバーによって生成されたデータブロックをパススルーするために使用されます。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>[購入]</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>[はい]</p></td>
<td><p>[はい]</p></td>
<td><p>フィルター</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>PVOID</p></td>
</tr>
</tbody>
</table>

 

プロパティ値 (操作データ) は PVOID 型です。これは、ミニドライバーによって生成されたデータブロックのユーザーモードバッファーへのポインターです。

### <a name="comments"></a>コメント

プロパティ get 呼び出し:

アプリケーションが長さ0のバッファーを使用してプロパティ get 呼び出しを行う場合、ミニドライバーは状態\_バッファー\_オーバーフローを返し、 **Irp-&gt;IoStatus. 情報**フィールドに必要なバッファーサイズを指定する必要があります。 長さのバッファーが0以外の場合、ミニドライバーは、指定されたバッファーがデータブロックに対して小さすぎる場合に、ステータス\_バッファー\_\_小さすぎる必要があります。それ以外の場合、ミニドライバーは、後で復元できるデータブロックに設定をパックします。

データの整合性チェックは、データを生成したミニドライバーを示す一意の GUID、巡回冗長検査 (CRC)、ヘッダー長など、データにミニドライバーが追加する必要があります。

返されるデータは軽量であり、現在の設定を再構築するために必要な情報のみが含まれている必要があります。

アプリケーションでは、複数レベルの undos にこのプロパティが使用され、プロジェクトに格納されます。

プロパティセットの呼び出し:

ミニドライバーは、データの整合性を検証し、データブロックのサイズが最大データサイズ (たとえば、特定のサイズを超えてすべてを拒否するなど) であることを確認する必要があります。 また、CRC とヘッダーの長さも検証する必要があります。 また、ミニドライバーは、 [CODECAPI\_currentchangelist](codecapi-currentchangelist.md)に反映されるすべての変更をキャッシュする必要があります。

### <a name="requirements"></a>要件

**ヘッダー:** *Ksmedia. h*で宣言されています。 *Ksmedia. h*をインクルードします。

### <a name="see-also"></a>参照

[**Ksk プロパティ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)、 [CODECAPI\_currentchangelist](codecapi-currentchangelist.md)リスト

 

 





