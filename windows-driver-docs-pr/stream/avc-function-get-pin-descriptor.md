---
title: AVC\_関数\_取得\_PIN\_記述子
description: AVC\_関数\_取得\_PIN\_記述子
ms.assetid: 1a02c328-e908-4125-abe7-4db9970ac86a
keywords:
- AVC_FUNCTION_GET_PIN_DESCRIPTOR ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- AVC_FUNCTION_GET_PIN_DESCRIPTOR
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 43cb459217c39a6fd4197b3c27fef287d3303e75
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386739"
---
# <a name="avcfunctiongetpindescriptor"></a>AVC\_関数\_取得\_PIN\_記述子


## <span id="ddk_avc_function_get_pin_descriptor_ks"></span><span id="DDK_AVC_FUNCTION_GET_PIN_DESCRIPTOR_KS"></span>


**AVC\_関数\_取得\_PIN\_記述子**関数コードが各暗証番号 (pin) の ID (0 からのオフセット) の暗証番号 (pin) の記述子を取得します。

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

この関数を使用して、 **PinDescriptor** 、AVC のメンバー\_MULTIFUNC\_IRB 構造の下に示すようにします。

```cpp
typedef struct _AVC_MULTIFUNC_IRB {
  AVC_IRB  Common;
  union {
    .
    .
    .
    AVC_PIN_DESCRIPTOR PinDescriptor;
 .
    .
    .
  };
} AVC_MULTIFUNC_IRB, *PAVC_MULTIFUNC_IRB;
```

### <a name="requirements"></a>要件

**ヘッダー:** 宣言されている*avc.h*します。 含める*avc.h*します。

### <a name="avcmultifuncirb-input"></a>AVC\_MULTIFUNC\_IRB 入力

**一般的です**  
**関数**にこのメンバーのサブメンバーを設定する必要があります**AVC\_関数\_取得\_PIN\_記述子**、AVC から\_関数の列挙体です。

<span id="PinDescriptor"></span><span id="pindescriptor"></span><span id="PINDESCRIPTOR"></span>**PinDescriptor**  
AV/C サブユニット デバイスで pin の説明を指定します。

仮想インスタンスでは、この関数のコードはサポートされていない*avc.sys*します。

だけでなく、暗証番号 (pin) の記述子この関数は、intersect ハンドラーと intersect ハンドラーに関連付けられた非透過のコンテキスト値のアドレスを返すも可能性があります。 Intersect ハンドラーのメンバーがある場合**NULL**、サブユニット ドライバーが交差するハンドラーを提供する必要があります。 Intersect ハンドラーのメンバーでない場合**NULL**intersect ハンドラーが提供される、ドライバーを使用することができます。

*Avc.sys*することはありませんが、データの積集合をフィルター ドライバー (たとえば、 *avcstrm.sys*) スタックをバックアップする要求が完了されるよう入力します。

これは、IRQL で呼び出す必要がある = パッシブ\_レベル。

### <a name="see-also"></a>関連項目

[**AVC\_MULTIFUNC\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avc_multifunc_irb)、 [ **AVC\_PIN\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avc_pin_descriptor)、 [ **AVC\_関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ne-avc-_tagavc_function)、 [ **KSPIN\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspin_descriptor)、 [ **AV/C 交差ハンドラー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/nc-avc-pfnavcintersecthandler)

 

 





