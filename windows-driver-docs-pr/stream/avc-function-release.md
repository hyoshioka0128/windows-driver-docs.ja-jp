---
title: AVC\_関数\_リリース
description: AVC\_関数\_リリース
ms.assetid: 77a35af2-ddf4-454b-a3a9-f5b7312fa64a
keywords:
- AVC_FUNCTION_RELEASE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- AVC_FUNCTION_RELEASE
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4731797ae0d58c954cd18a12eece016690c4428
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845074"
---
# <a name="avc_function_release"></a>AVC\_関数\_リリース


## <span id="ddk_avc_function_release_ks"></span><span id="DDK_AVC_FUNCTION_RELEASE_KS"></span>


**Avc\_関数\_リリース**関数のコードにより、 *avc*は、キャッシュされた avcconnectinfo 値によって提案されたすべての接続を解放します。

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

この関数は、次に示すように、AVC\_MULTIFUNC\_IRB 構造体の**Pinid**メンバーを使用します。

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

### <a name="requirements"></a>要件

**ヘッダー:** *Avc*で宣言されています。 *Avc. h*を含めます。

### <a name="avc_multifunc_irb-input"></a>AVC\_MULTIFUNC\_IRB 入力

**的**  
このメンバーの**関数**サブメンバーは、AVC\_関数の列挙から、 **avc\_関数\_リリース**に設定する必要があります。

**PinId**  
接続を解放するピンのオフセット (または ID) を指定します。

この関数コードは、 *avc*の仮想インスタンスではサポートされていません。

サブユニットドライバは、ピンが非アクティブになると、この機能を使用する必要があります。

これは、IRQL = パッシブ\_レベルで呼び出す必要があります。

### <a name="see-also"></a>参照

[**Avc\_MULTIFUNC\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_multifunc_irb)、 [**avc\_PIN\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_pin_id)、 [**avc\_関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)

 

 





