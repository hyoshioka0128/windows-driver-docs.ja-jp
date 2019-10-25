---
title: AVC\_関数\_\_EXT\_プラグ\_数を取得します
description: AVC\_関数\_\_EXT\_プラグ\_数を取得します
ms.assetid: dced18ac-dc26-4c47-bc92-a3f3daec505b
keywords:
- AVC_FUNCTION_GET_EXT_PLUG_COUNTS ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- AVC_FUNCTION_GET_EXT_PLUG_COUNTS
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e633c45f67e6ea7af0dfbef327a94e15e63f3bff
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844657"
---
# <a name="avc_function_get_ext_plug_counts"></a>AVC\_関数\_\_EXT\_プラグ\_数を取得します


## <span id="ddk_avc_function_get_ext_plug_counts_ks"></span><span id="DDK_AVC_FUNCTION_GET_EXT_PLUG_COUNTS_KS"></span>


**AVC\_関数は\_EXT\_の\_のプラグ\_カウント**関数のコードを取得して、外部入力と出力プラグの数を取得します。

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

この関数は、次に示すように、AVC\_MULTIFUNC\_IRB 構造体の**ExtPlugCounts**メンバーを使用します。

```cpp
typedef struct _AVC_MULTIFUNC_IRB {
  AVC_IRB  Common;
  union {
    .
    .
    .
    AVC_EXT_PLUG_COUNTS ExtPlugCounts;
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
このメンバーの**関数**submember は、AVC\_関数の列挙から **\_EXT\_の\_を取得**するために、avc\_関数に設定されている必要があります。

<span id="ExtPlugCounts"></span><span id="extplugcounts"></span><span id="EXTPLUGCOUNTS"></span>**ExtPlugCounts**  
外部入力プラグと出力プラグの数を指定します。

この関数コードは、 *avc*の仮想インスタンスではサポートされていません。

サブユニットドライバーは、外部プラグの機能、形式、および使用方法を決定する役割を担います。 ただし、 *avc*では、外部プラグとサブユニットの間の永続的な接続が、サブユニットの専用のピンとして報告されます (詳細については、「 [**Avc\_関数\_\_CONNECTINFO を取得**](avc-function-get-connectinfo.md)する」を参照してください)。

これは、IRQL = パッシブ\_レベルで呼び出す必要があります。

### <a name="see-also"></a>参照

[**Avc\_MULTIFUNC\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_multifunc_irb)、 [**avc\_EXT\_プラグ\_数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_ext_plug_counts)、 [**avc\_関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)

 

 





