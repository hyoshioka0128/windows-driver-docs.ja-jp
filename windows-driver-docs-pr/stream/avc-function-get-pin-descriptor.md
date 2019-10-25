---
title: AVC\_関数\_取得\_PIN\_記述子
description: AVC\_関数\_取得\_PIN\_記述子
ms.assetid: 1a02c328-e908-4125-abe7-4db9970ac86a
keywords:
- AVC_FUNCTION_GET_PIN_DESCRIPTOR ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- AVC_FUNCTION_GET_PIN_DESCRIPTOR
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5f83d98c9ae7493dd6a557554b12dc55c5c0ed5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845083"
---
# <a name="avc_function_get_pin_descriptor"></a>AVC\_関数\_取得\_PIN\_記述子


## <span id="ddk_avc_function_get_pin_descriptor_ks"></span><span id="DDK_AVC_FUNCTION_GET_PIN_DESCRIPTOR_KS"></span>


**AVC\_関数\_GET\_pin\_記述子**関数のコードは、各 pin ID (0 からのオフセット) の pin 記述子を取得します。

### <a name="io-status-block"></a>I/O ステータス ブロック

成功した場合、AV/C プロトコルドライバーは、 **Irp&gt;iostatus. status**を STATUS\_SUCCESS に設定します。

その他の戻り値には次のようなものがあります。

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
<td><p>要求が行われましたが、すべてのタイムアウトと再試行処理が完了する前に応答が受信されませんでした。</p></td>
</tr>
<tr class="even">
<td><p>STATUS_REQUEST_ABORTED</p></td>
<td><p>IRP の完了状態が STATUS_REQUEST_ABORTED になるとすぐに中止します。 これは、デバイスが削除されたか、1394バスで使用できなくなったことを示します。</p></td>
</tr>
<tr class="odd">
<td><p>STATUS_*</p></td>
<td><p>その他のリターンコードは、AV/C プロトコルの範囲を超えてエラーまたは警告が発生したことを示します。</p></td>
</tr>
</tbody>
</table>

 

### <a name="comments"></a>コメント

この関数は、次に示すように、AVC\_MULTIFUNC\_IRB 構造体の**Pindescriptor**メンバーを使用します。

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

**ヘッダー:** *Avc*で宣言されています。 *Avc. h*を含めます。

### <a name="avc_multifunc_irb-input"></a>AVC\_MULTIFUNC\_IRB 入力

**的**  
このメンバーの**関数**submember は、AVC\_関数の列挙から **\_記述子を取得\_\_、avc\_関数**に設定されている必要があります。

<span id="PinDescriptor"></span><span id="pindescriptor"></span><span id="PINDESCRIPTOR"></span>**PinDescriptor**  
AV/C サブユニットデバイスのピンの説明を指定します。

この関数コードは、 *avc*の仮想インスタンスではサポートされていません。

この関数は、ピン記述子に加えて、intersect ハンドラーと、intersect ハンドラーに関連付けられている不透明なコンテキスト値も返すことがあります。 Intersect ハンドラーメンバーが**NULL**の場合、サブユニットドライバーは intersect ハンドラーを提供する必要があります。 Intersect ハンドラーのメンバーが**NULL**でない場合は、intersect ハンドラーが指定され、ドライバーがそれを使用する可能性があります。

*Avc*ではデータの積集合は提供されませんが、フィルタードライバー ( *avcstrm .sys*など) では、要求がスタックを通じてバックアップされるため、フィルタードライバーによって入力されます。

これは、IRQL = パッシブ\_レベルで呼び出す必要があります。

### <a name="see-also"></a>参照

[**Avc\_MULTIFUNC\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_multifunc_irb)、 [**avc\_PIN\_記述子**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_pin_descriptor)、 [**avc\_関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)、 [**Kspin\_DESCRIPTOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)、 [**AV/C Intersect ハンドラー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/nc-avc-pfnavcintersecthandler)

 

 





