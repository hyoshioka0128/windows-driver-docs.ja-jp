---
title: CODECAPI\_SETALLDEFAULTS
description: CODECAPI\_SETALLDEFAULTS
ms.assetid: 6a50a75f-cbc5-487f-b2cd-34e89eb127a0
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 227c525dd078f6167c386a43aeab613e9af3a44c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56532315"
---
# <a name="codecapisetalldefaults"></a>CODECAPI\_SETALLDEFAULTS


## <span id="ddk_codecapi_setalldefaults_ks"></span><span id="DDK_CODECAPI_SETALLDEFAULTS_KS"></span>


CODECAPI\_SETALLDEFAULTS プロパティは、ミニドライバーのすべての内部設定を既定の構成にリセットするために使用します。

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
<td><p>X</p></td>
<td><p>〇</p></td>
<td><p>フィルター</p></td>
<td><p>KSPROPERTY</p></td>
<td><p>なし</p></td>
</tr>
</tbody>
</table>

 

このプロパティを設定するセットが、デバイスが既定値にそのすべての設定にリセット トリガーで。

### <a name="comments"></a>コメント

パラメーターの変更のリスト全体をキャッシュする必要があります、ミニドライバー [CODECAPI\_CURRENTCHANGELIST](codecapi-currentchangelist.md)このプロパティが設定されている場合。

### <a name="requirements"></a>要件

**ヘッダー:** 宣言されている*ksmedia.h*します。 含める*ksmedia.h*します。

### <a name="see-also"></a>参照

[**KSPROPERTY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksidentifier)

 

 





