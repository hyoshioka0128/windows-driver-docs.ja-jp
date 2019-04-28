---
title: CODECAPI\_ALLSETTINGS
description: CODECAPI\_ALLSETTINGS
ms.assetid: 0ae11200-af21-476a-89a8-515bd98920a0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 635cfa5aecfacaa7ff1ba5200196dd290949c509
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374208"
---
# <a name="codecapiallsettings"></a>CODECAPI\_ALLSETTINGS


## <span id="ddk_codecapi_allsettings_ks"></span><span id="DDK_CODECAPI_ALLSETTINGS_KS"></span>


CODECAPI\_ミニドライバーで生成されたデータ ブロックを前後へ渡す ALLSETTINGS プロパティを使用します。

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
<th>取得</th>
<th>設定</th>
<th>対象</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>〇</p></td>
<td><p>〇</p></td>
<td><p>フィルター</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>PVOID</p></td>
</tr>
</tbody>
</table>

 

プロパティの値 (データの操作) は、型、PVOID ミニドライバーで生成されたデータ ブロックのユーザー モード バッファーへのポインターであるは。

### <a name="comments"></a>コメント

プロパティの呼び出しを取得します。

アプリケーションが 0 個の長バッファーを使用して呼び出しを取得するプロパティを行った場合、ミニドライバーは状態を返す必要があります\_バッファー\_OVERFLOW で必要なバッファー サイズを指定して、 **Irp-&gt;IoStatus.Information**フィールド。 バッファーの長さが 0 以外の場合、ミニドライバーは状態を返す必要があります\_バッファー\_すぎます\_小規模の指定されたバッファーが小さすぎる場合、データ ブロックのそれ以外の場合、ミニドライバーのパック データ ブロックには、その設定を指定できます後で復元します。

データの整合性を追加するミニドライバーの責任は、データ、巡回冗長検査 (CRC)、およびヘッダーの長さ、ミニドライバーが生成されるかを示す一意の GUID など、データを確認します。

返されるデータは、軽量し、現在の設定を再構築に必要な情報のみを含めることが必要があります。

アプリケーションでは、このプロパティを使用して、複数レベルの取り消し、そのプロジェクトで格納されているのです。

プロパティの呼び出しを設定します。

ミニドライバーは、データの整合性を検証する必要があり、チェックするデータ ブロック サイズが最大データ サイズ未満 (たとえば、ものすべてを拒否一定のサイズを超える)。 また、CRC とヘッダーの長さも確認してください。 ミニドライバーに反映される変更をキャッシュする必要がありますも[CODECAPI\_CURRENTCHANGELIST](codecapi-currentchangelist.md)します。

### <a name="requirements"></a>必要条件

**ヘッダー:** 宣言されている*ksmedia.h*します。 含める*ksmedia.h*します。

### <a name="see-also"></a>関連項目

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)、 [CODECAPI\_CURRENTCHANGELIST](codecapi-currentchangelist.md)

 

 





