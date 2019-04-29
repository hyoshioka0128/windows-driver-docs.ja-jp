---
title: AVC\_関数\_設定\_接続情報
description: AVC\_関数\_設定\_接続情報
ms.assetid: e97b525a-2236-44a9-9d49-dc0df760f21e
keywords:
- AVC_FUNCTION_SET_CONNECTINFO ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- AVC_FUNCTION_SET_CONNECTINFO
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23d6016942535b915b4bd9654b80b4beee1d9f08
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390192"
---
# <a name="avcfunctionsetconnectinfo"></a>AVC\_関数\_設定\_接続情報


## <span id="ddk_avc_function_set_connectinfo_ks"></span><span id="DDK_AVC_FUNCTION_SET_CONNECTINFO_KS"></span>


AVC\_関数\_設定\_CONNECT\_情報関数のコードは、暗証番号 (pin) ID (0 からのオフセット) ごとに AVCCONNECTINFO 構造体を設定します。

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

この関数を使用して、 **SetConnectInfo** 、AVC のメンバー\_MULTIFUNC\_IRB 構造の下に示すようにします。

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

### <a name="requirements"></a>必要条件

**ヘッダー:** 宣言されている*avc.h*します。 含める*avc.h*します。

### <a name="avcmultifuncirb-input"></a>AVC\_MULTIFUNC\_IRB 入力

**一般的です**  
**関数**にこのメンバーのサブメンバーを設定する必要があります**AVC\_関数\_設定\_接続情報**、AVC から\_関数の列挙体。

<span id="SetConnectInfo"></span><span id="setconnectinfo"></span><span id="SETCONNECTINFO"></span>**SetConnectInfo**  
AV/C デバイスの接続情報を指定します。

仮想インスタンスでは、この関数のコードはサポートされていない*avc.sys*します。

サブユニット ドライバーは、intersect ハンドラーを提供する場合、この関数を使用する必要があります。 AVCCONNECTINFO 構造 (、AVC 内に含まれる\_設定\_接続情報の構造) は、intersect ハンドラーに渡されるデータの範囲に追加される AVCPRECONNECTINFO 構造から派生します。

データの範囲に互換性があることを決定した後は、intersect ハンドラーは、AVCCONNECTINFO 構造を生成します。 この構造体は、結果のデータ形式に追加されにも送信*avc.sys*します。 これは必要ありません、提案されたデータの形式が後より良いもの渡された場合ため*avc.sys* AVCCONNECTINFO 構造体の 1 つのキャッシュだけです。

これは、IRQL で呼び出す必要がある = パッシブ\_レベル。

### <a name="see-also"></a>関連項目

[**AVC\_MULTIFUNC\_IRB**](https://msdn.microsoft.com/library/windows/hardware/ff554177)、 [ **AVC\_SETCONNECT\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff554192)、 [ **AVCCONNECTINFO**](https://msdn.microsoft.com/library/windows/hardware/ff554101)、 [ **AVC\_関数**](https://msdn.microsoft.com/library/windows/hardware/ff554145)、 [ **AV/C 交差ハンドラー**](https://msdn.microsoft.com/library/windows/hardware/ff556379)

 

 





