---
title: AVC\_関数\_取得
description: AVC\_関数\_取得
ms.assetid: c250d800-1777-44c0-8902-09017eb46c78
keywords:
- AVC_FUNCTION_ACQUIRE ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- AVC_FUNCTION_ACQUIRE
api_type:
- NA
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1c791ee2fed6aeb71aadd6cdb3f47b51ef4cfda2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845161"
---
# <a name="avc_function_acquire"></a>AVC\_関数\_取得

**Avc\_関数\_** 関数コードを取得すると、 *avc*は、キャッシュされた avcconnectinfo 値によって提案された接続を確立します。

## <a name="io-status-block"></a>I/O ステータス ブロック

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

## <a name="comments"></a>コメント

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

## <a name="requirements"></a>要件

**ヘッダー:** *Avc*で宣言されています。 *Avc. h*を含めます。

## <a name="avc_multifunc_irb-input"></a>AVC\_MULTIFUNC\_IRB 入力

**的**  

このメンバーの**関数**submember は、AVC\_関数の列挙から**取得\_avc\_関数**に設定されている必要があります。

**PinId**  

接続を取得するピンのオフセット (または ID) を指定します。

この関数コードは、 *avc*の仮想インスタンスではサポートされていません。

サブユニットドライバは、ピンがアクティブになったときに、この機能を使用する必要があります。

これは、IRQL = パッシブ\_レベルで呼び出す必要があります。

## <a name="see-also"></a>参照

[**AVC\_MULTIFUNC\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_multifunc_irb)

[**AVC\_PIN\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_pin_id)

[**AVC\_関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)
