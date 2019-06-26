---
title: AVC\_関数\_取得\_接続情報
description: AVC\_関数\_取得\_接続情報
ms.assetid: d4230024-a765-47f0-9958-9f71761f7b85
keywords:
- AVC_FUNCTION_GET_CONNECTINFO ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- AVC_FUNCTION_GET_CONNECTINFO
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e41a31a569ffdfdab67fe415b49b2106ebe95d14
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386753"
---
# <a name="avcfunctiongetconnectinfo"></a>AVC\_関数\_取得\_接続情報


## <span id="ddk_avc_function_get_connectinfo_ks"></span><span id="DDK_AVC_FUNCTION_GET_CONNECTINFO_KS"></span>


AVC\_関数\_取得\_CONNECT\_情報関数のコードは、各暗証番号 (pin) の id (0 からのオフセット) AVCPRECONNECTINFO 構造体を取得します。

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

この関数を使用して、 **PreConnectInfo** 、AVC のメンバー\_MULTIFUNC\_IRB 構造の下に示すようにします。

```cpp
typedef struct _AVC_MULTIFUNC_IRB {
  AVC_IRB  Common;
  union {
    .
    .
    .
    AVC_PRECONNECT_INFO PreConnectInfo;
 .
    .
    .
  };
} AVC_MULTIFUNC_IRB, *PAVC_MULTIFUNC_IRB;
```

メンバー、AVC の\_ダイヤル\_情報構造体を以下に示します。

```cpp
typedef struct _AVC_PRECONNECT_INFO {
    IN ULONG PinId
    OUT AVCPRECONNECTINFO ConnectInfo;
} AVC_PRECONNECT_INFO, *PAVC_PRECONNECT_INFO;
```

### <a name="requirements"></a>必要条件

**ヘッダー:** 宣言されている*avc.h*します。 含める*avc.h*します。

### <a name="avcmultifuncirb-input"></a>AVC\_MULTIFUNC\_IRB 入力

**一般的です**  
**関数**にこのメンバーのサブメンバーを設定する必要があります**AVC\_関数\_取得\_接続情報**、AVC から\_関数の列挙体。

<span id="ConnectInfo"></span><span id="connectinfo"></span><span id="CONNECTINFO"></span>**接続情報**  
AV/C デバイスの接続情報を指定します。

仮想インスタンスでは、この関数のコードはサポートされていない*avc.sys*します。

サブユニット ドライバーが、KSPIN に含まれるデータの範囲を作成する場合にこの関数を使用する必要があります\_記述子構造体。 AVCPRECONNECTINFO 構造に追加、 **DataRanges** PC の外部接続用メンバー。

これは、IRQL で呼び出す必要がある = パッシブ\_レベル。

### <a name="see-also"></a>関連項目

[**AVC\_MULTIFUNC\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avc_multifunc_irb), [**AVC\_PRECONNECT\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avc_preconnect_info), [**AVCPRECONNECTINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avcpreconnectinfo), [**AVC\_FUNCTION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ne-avc-_tagavc_function)

 

 





