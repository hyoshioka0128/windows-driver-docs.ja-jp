---
title: AVC\_関数\_取得\_UNIQUE\_ID
description: AVC\_関数\_取得\_UNIQUE\_ID
ms.assetid: 51b35686-03a9-45b3-8bdc-14cbd24714dc
keywords:
- AVC_FUNCTION_GET_UNIQUE_ID ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- AVC_FUNCTION_GET_UNIQUE_ID
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e803243b434410b8711c2a357c2ad498e8c9df28
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56578501"
---
# <a name="avcfunctiongetuniqueid"></a>AVC\_関数\_取得\_UNIQUE\_ID


## <span id="ddk_avc_function_get_unique_id_ks"></span><span id="DDK_AVC_FUNCTION_GET_UNIQUE_ID_KS"></span>


**AVC\_関数\_取得\_UNIQUE\_ID**関数のコードは、AV/C 単位の一意の ID を取得します。

### <a name="io-status-block"></a>I/O ステータス ブロック

成功すると、AV/C をプロトコル ドライバーに設定**Irp -&gt;IoStatus.Status**ステータス\_成功します。

その他の戻り値には、考えられる。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>戻り値</th>
<th>説明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>STATUS_TIMEOUT</p></td>
<td><p>要求が行われたが、すべてタイムアウトするまでの応答が受信されず、再試行の処理が完了します。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_REQUEST_ABORTED</p></td>
<td><p>IRP の完了ステータスが STATUS_REQUEST_ABORTED がすぐに中止します。 これは、デバイスが削除されたかは、1394 バスで使用できなくすることを示します。</p></td>
</tr>
<tr class="odd">
<td><p>STATUS_*</p></td>
<td><p>他のリターン コードでは、エラーまたは警告が発生したこと、AV/C プロトコルの範囲を超えていたことを示します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="comments"></a>コメント

この関数を使用して、 **UniqueID** 、AVC のメンバー\_MULTIFUNC\_IRB 構造の下に示すようにします。

```cpp
typedef struct _AVC_MULTIFUNC_IRB {
  AVC_IRB  Common;
  union {
    .
    .
    .
    AVC_UNIQUE_ID UniqueID;
 .
    .
    .
  };
} AVC_MULTIFUNC_IRB, *PAVC_MULTIFUNC_IRB;
```

メンバーの AVC\_UNIQUE\_ID の構造を以下に示します。

```cpp
typedef struct _AVC_UNIQUE_ID {
    OUT GUID DeviceID;
} AVC_UNIQUE_ID, *PAVC_UNIQUE_ID;
```

### <a name="requirements"></a>必要条件

**ヘッダー:** 宣言されている*avc.h*します。 含める*avc.h*します。

### <a name="avcmultifuncirb-input"></a>AVC\_MULTIFUNC\_IRB 入力

**一般的です**  
**関数**にこのメンバーのサブメンバーを設定する必要があります**AVC\_関数\_取得\_UNIQUE\_ID** 、AVC から\_関数列挙体です。

<span id="UniqueID"></span><span id="uniqueid"></span><span id="UNIQUEID"></span>**一意の Id**  
全体として単位を表す GUID を指定します。 同じ単位内のすべてのサブユニットでは、同じ GUID を共有します。 同じ GUID を共有する 2 つのユニットではありません。

仮想インスタンスでは、この関数のコードはサポートされていない*avc.sys*します。

サブユニット ドライバーが (同じユニットに属しているアプリケーションを多数のサブユニット ドライバーのインスタンスのバージョンの確認する必要があります) 管理アプリケーションをデバイスの GUID を報告する必要がある場合、または構築している独自の AVCPRECONNECTINFO 構造の場合、この関数を使用します。外部プラグインするときにします。

これは、IRQL で呼び出す必要がある = パッシブ\_レベル。

### <a name="see-also"></a>関連項目

[**AVC\_MULTIFUNC\_IRB**](https://msdn.microsoft.com/library/windows/hardware/ff554177)、 [ **AVC\_UNIQUE\_ID**](https://msdn.microsoft.com/library/windows/hardware/ff554200)、 [ **AVCPRECONNECTINFO**](https://msdn.microsoft.com/library/windows/hardware/ff554103)、 [ **AVC\_関数**](https://msdn.microsoft.com/library/windows/hardware/ff554145)

 

 





