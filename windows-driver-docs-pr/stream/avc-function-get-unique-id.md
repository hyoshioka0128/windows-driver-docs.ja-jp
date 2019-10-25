---
title: AVC\_関数\_\_一意の\_ID を取得します
description: AVC\_関数\_\_一意の\_ID を取得します
ms.assetid: 51b35686-03a9-45b3-8bdc-14cbd24714dc
keywords:
- AVC_FUNCTION_GET_UNIQUE_ID ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- AVC_FUNCTION_GET_UNIQUE_ID
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90618cbbbd5b2d463130e93fea9b812367cf6899
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845077"
---
# <a name="avc_function_get_unique_id"></a>AVC\_関数\_\_一意の\_ID を取得します


## <span id="ddk_avc_function_get_unique_id_ks"></span><span id="DDK_AVC_FUNCTION_GET_UNIQUE_ID_KS"></span>


**AVC\_関数\_\_一意の\_id**関数コードを取得して、AV/C ユニットの一意の id を取得します。

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

この関数は、次に示すように、AVC\_MULTIFUNC\_IRB 構造体の**UniqueID**メンバーを使用します。

```cpp
typedef struct _AVC_MULTIFUNC_IRB {
  AVC_IRB  Common;
  union {
    .
    .
    .
    AVC_UNIQUE_ID UniqueID;
 .
    .
    .
  };
} AVC_MULTIFUNC_IRB, *PAVC_MULTIFUNC_IRB;
```

AVC\_固有の\_ID 構造体のメンバーを次に示します。

```cpp
typedef struct _AVC_UNIQUE_ID {
    OUT GUID DeviceID;
} AVC_UNIQUE_ID, *PAVC_UNIQUE_ID;
```

### <a name="requirements"></a>要件

**ヘッダー:** *Avc*で宣言されています。 *Avc. h*を含めます。

### <a name="avc_multifunc_irb-input"></a>AVC\_MULTIFUNC\_IRB 入力

**的**  
このメンバーの**関数**submember は、AVC\_関数の列挙から**一意の\_ID を取得\_\_、avc\_関数**に設定されている必要があります。

<span id="UniqueID"></span><span id="uniqueid"></span><span id="UNIQUEID"></span>**UniqueID**  
単位を全体として表す GUID を指定します。 同じユニット内のすべてのサブユニットが同じ GUID を共有しています。 2つのユニットで同じ GUID を共有することはできません。

この関数コードは、 *avc*の仮想インスタンスではサポートされていません。

サブユニットドライバーでは、デバイスの GUID を、制御しているアプリケーション (多くのサブユニットのドライバーインスタンスが同じ単位に属していることを認識する必要があるアプリケーション) に報告する必要がある場合、または、外部プラグ。

これは、IRQL = パッシブ\_レベルで呼び出す必要があります。

### <a name="see-also"></a>参照

[**Avc\_MULTIFUNC\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_multifunc_irb)、 [**avc\_一意\_ID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_unique_id)、 [**avcpreconnectinfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avcpreconnectinfo)、 [**avc\_関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)

 

 





