---
title: AVC\_関数\_取得
description: AVC\_関数\_取得
ms.assetid: c250d800-1777-44c0-8902-09017eb46c78
keywords:
- AVC_FUNCTION_ACQUIRE ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- AVC_FUNCTION_ACQUIRE
api_type:
- NA
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9edc1b2a8c1a7bd970a369b4068c27b71b083b0d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386749"
---
# <a name="avcfunctionacquire"></a>AVC\_関数\_取得

**AVC\_関数\_ACQUIRE**関数のコードが*avc.sys* AVCCONNECTINFO のキャッシュされた値によって示されたすべての接続を確立します。

## <a name="io-status-block"></a>I/O ステータス ブロック

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

## <a name="comments"></a>コメント

この関数を使用して、 **PinId** 、AVC のメンバー\_MULTIFUNC\_IRB 構造の下に示すようにします。

```cpp
typedef struct _AVC_MULTIFUNC_IRB {
  AVC_IRB  Common;
  union {
    .
    .
    .
    AVC_PIN_ID PinId;
 .
    .
    .
  };
} AVC_MULTIFUNC_IRB, *PAVC_MULTIFUNC_IRB;
```

## <a name="requirements"></a>必要条件

**ヘッダー:** 宣言されている*avc.h*します。 含める*avc.h*します。

## <a name="avcmultifuncirb-input"></a>AVC\_MULTIFUNC\_IRB 入力

**一般的です**  

**関数**にこのメンバーのサブメンバーを設定する必要があります**AVC\_関数\_ACQUIRE** 、AVC から\_関数の列挙体。

**PinId**  

接続が取得される pin のオフセット (または ID) を指定します。

仮想インスタンスでは、この関数のコードはサポートされていない*avc.sys*します。

サブユニット ドライバーは、暗証番号 (pin) がアクティブになったとき、この関数を使用する必要があります。

これは、IRQL で呼び出す必要がある = パッシブ\_レベル。

## <a name="see-also"></a>関連項目

[**AVC\_MULTIFUNC\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avc_multifunc_irb)

[**AVC\_PIN\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avc_pin_id)

[**AVC\_関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ne-avc-_tagavc_function)
