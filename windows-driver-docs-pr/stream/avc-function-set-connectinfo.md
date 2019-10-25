---
title: '\_CONNECTINFO\_設定する AVC\_関数'
description: '\_CONNECTINFO\_設定する AVC\_関数'
ms.assetid: e97b525a-2236-44a9-9d49-dc0df760f21e
keywords:
- AVC_FUNCTION_SET_CONNECTINFO ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- AVC_FUNCTION_SET_CONNECTINFO
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27f3d40afa90e1a607b246731dcd1a6d67095c85
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845069"
---
# <a name="avc_function_set_connectinfo"></a>\_CONNECTINFO\_設定する AVC\_関数


## <span id="ddk_avc_function_set_connectinfo_ks"></span><span id="DDK_AVC_FUNCTION_SET_CONNECTINFO_KS"></span>


AVC\_関数\_SET\_CONNECT\_INFO 関数コードは、各 pin ID (0 からのオフセット) の AVCCONNECTINFO 構造体を設定します。

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

この関数は、次に示すように、AVC\_MULTIFUNC\_IRB 構造体の**Setconnectinfo**メンバーを使用します。

```cpp
typedef struct _AVC_MULTIFUNC_IRB {
  AVC_IRB  Common;
  union {
    .
    .
    .
    AVC_SETCONNECT_INFO SetConnectInfo;
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
このメンバーの**関数**サブメンバーは、AVC\_関数列挙体 **\_connectinfo に設定\_、avc\_関数**に設定されている必要があります。

<span id="SetConnectInfo"></span><span id="setconnectinfo"></span><span id="SETCONNECTINFO"></span>**SetConnectInfo**  
AV/C デバイスの接続情報を指定します。

この関数コードは、 *avc*の仮想インスタンスではサポートされていません。

サブユニットドライバーで intersect ハンドラーが指定されている場合は、この関数を使用する必要があります。 AVCCONNECTINFO 構造体 (AVC\_SET\_CONNECTINFO 構造体) は、intersect ハンドラーに渡されるデータ範囲に追加される AVCPRECONNECTINFO 構造体から派生します。

データ範囲に互換性があることを確認した後、intersect ハンドラーは AVCCONNECTINFO 構造体を生成します。 この構造体は、結果のデータ形式に追加され、 *avc*にも送信されます。 指定されたデータ形式がより良いものになるかどうかは問題ではありません。 *avc*は1つの AVCCONNECTINFO 構造体のみをキャッシュするためです。

これは、IRQL = パッシブ\_レベルで呼び出す必要があります。

### <a name="see-also"></a>参照

[**Avc\_MULTIFUNC\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_multifunc_irb)、 [**AVC\_SETCONNECT\_info**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_setconnect_info)、 [**avcconnectinfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avcconnectinfo)、 [**Avc\_FUNCTION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)、 [**AV/C Intersect ハンドラー**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/nc-avc-pfnavcintersecthandler)

 

 





