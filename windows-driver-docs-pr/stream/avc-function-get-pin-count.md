---
title: AVC\_関数\_取得\_PIN\_数
description: AVC\_関数\_取得\_PIN\_数
ms.assetid: fb455843-c979-479c-ba7c-f84875a9ba6f
keywords:
- AVC_FUNCTION_GET_PIN_COUNT ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- AVC_FUNCTION_GET_PIN_COUNT
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d71361da9d9c7675e0804f02f25e0ad8f2b35bad
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386741"
---
# <a name="avcfunctiongetpincount"></a>AVC\_関数\_取得\_PIN\_数


## <span id="ddk_avc_function_get_pin_count_ks"></span><span id="DDK_AVC_FUNCTION_GET_PIN_COUNT_KS"></span>


**AVC\_関数\_取得\_PIN\_カウント**関数のコードは、基になるサブユニット デバイスでサポートされている pin の数を取得します。

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

この関数を使用して、 **PinCount** 、AVC のメンバー\_MULTIFUNC\_IRB 構造の下に示すようにします。

```cpp
typedef struct _AVC_MULTIFUNC_IRB {
  AVC_IRB  Common;
  union {
    AVC_PIN_COUNT PinCount;
 .
    .
    .
  };
} AVC_MULTIFUNC_IRB, *PAVC_MULTIFUNC_IRB;
```

### <a name="requirements"></a>必要条件

**ヘッダー:** 宣言されている*avc.h*します。 含める*avc.h*します。

### <a name="avcmultifuncirb-input"></a>AVC\_MULTIFUNC\_IRB 入力

**一般的です**  
**関数**にこのメンバーのサブメンバーを設定する必要があります**AVC\_関数\_取得\_PIN\_カウント**、AVC から\_関数列挙体です。

<span id="PinCount"></span><span id="pincount"></span><span id="PINCOUNT"></span>**PinCount**  
関数から戻ると、AV/C デバイスで pin の数を指定します。

仮想インスタンスでは、この関数のコードはサポートされていない*avc.sys*します。

これは、IRQL で呼び出す必要がある = パッシブ\_レベル。

### <a name="see-also"></a>関連項目

[**AVC\_MULTIFUNC\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avc_multifunc_irb), [**AVC\_PIN\_COUNT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avc_pin_count), [**AVC\_FUNCTION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ne-avc-_tagavc_function)

 

 





