---
title: AVC\_関数\_\_CONNECTINFO を取得します
description: AVC\_関数\_\_CONNECTINFO を取得します
ms.assetid: d4230024-a765-47f0-9958-9f71761f7b85
keywords:
- AVC_FUNCTION_GET_CONNECTINFO ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- AVC_FUNCTION_GET_CONNECTINFO
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 799b48657c5e03ccec5c538426d7d01ad68a3119
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845157"
---
# <a name="avc_function_get_connectinfo"></a>AVC\_関数\_\_CONNECTINFO を取得します


## <span id="ddk_avc_function_get_connectinfo_ks"></span><span id="DDK_AVC_FUNCTION_GET_CONNECTINFO_KS"></span>


AVC\_関数\_GET\_CONNECT\_INFO 関数は、各 pin ID (0 からのオフセット) の AVCPRECONNECTINFO 構造体を取得します。

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

この関数は、次に示すように、AVC\_MULTIFUNC\_IRB 構造体の**Preconnectinfo**メンバーを使用します。

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

AVC\_PRECONNECT\_INFO 構造体のメンバーを次に示します。

```cpp
typedef struct _AVC_PRECONNECT_INFO {
    IN ULONG PinId
    OUT AVCPRECONNECTINFO ConnectInfo;
} AVC_PRECONNECT_INFO, *PAVC_PRECONNECT_INFO;
```

### <a name="requirements"></a>要件

**ヘッダー:** *Avc*で宣言されています。 *Avc. h*を含めます。

### <a name="avc_multifunc_irb-input"></a>AVC\_MULTIFUNC\_IRB 入力

**的**  
このメンバーの**関数**submember は、AVC\_関数列挙から**CONNECTINFO を\_取得\_には、avc\_関数**に設定する必要があります。

<span id="ConnectInfo"></span><span id="connectinfo"></span><span id="CONNECTINFO"></span>**ConnectInfo**  
AV/C デバイスの接続情報を指定します。

この関数コードは、 *avc*の仮想インスタンスではサポートされていません。

サブユニットドライバーは、KSPIN\_記述子構造に含まれるデータ範囲の作成を担当する場合に、この関数を使用する必要があります。 AVCPRECONNECTINFO 構造体は、PC 外部の接続の**DataRanges**メンバーに追加されます。

これは、IRQL = パッシブ\_レベルで呼び出す必要があります。

### <a name="see-also"></a>参照

[**Avc\_MULTIFUNC\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_multifunc_irb)、 [**avc\_PRECONNECT\_info**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_preconnect_info)、 [**avcpreconnectinfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avcpreconnectinfo)、 [**avc\_関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)

 

 





