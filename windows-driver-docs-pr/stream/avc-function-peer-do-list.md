---
title: '\_ピア\_DO\_リストの AVC\_関数'
description: '\_ピア\_DO\_リストの AVC\_関数'
ms.assetid: 80ffd94e-788f-4874-b716-3eb66d90e4aa
keywords:
- AVC_FUNCTION_PEER_DO_LIST ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- AVC_FUNCTION_PEER_DO_LIST
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac01e847714425e15a7875a7ab7a729b7caaf9ab
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845075"
---
# <a name="avc_function_peer_do_list"></a>\_ピア\_DO\_リストの AVC\_関数


## <span id="ddk_avc_function_peer_do_list_ks"></span><span id="DDK_AVC_FUNCTION_PEER_DO_LIST_KS"></span>


**Avc\_関数\_ピア\_DO\_LIST**関数のコードは、すべての非仮想*AVC*インスタンスを検索します。

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
<td><p>STATUS_INSUFFICIENT_RESOURCES</p></td>
<td><p>デバイスオブジェクト参照の一覧の領域を取得できませんでした。</p></td>
</tr>
</tbody>
</table>

 

### <a name="comments"></a>コメント

この関数は、次に示すように、AVC\_MULTIFUNC\_IRB 構造体の**PeerList**メンバーを使用します。

```cpp
typedef struct _AVC_MULTIFUNC_IRB {
  AVC_IRB  Common;
  union {
    .
    .
    .
    AVC_PEER_DO_LIST PeerList;
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
このメンバーの**関数**のサブメンバーは、AVC\_関数の列挙の **\_\_ピア\_DO\_関数**に設定する必要があります。

<span id="PeerList"></span><span id="peerlist"></span><span id="PEERLIST"></span>**PeerList**  
*Avc*の非仮想 (ピア) インスタンスすべてのリストを指定します。

呼び出し元は、オブジェクトリストに返されたいずれかのオブジェクトを介して、GUID\_AVC\_クラスのデバイスインターフェイス要求を送信できます。 呼び出し元は、( **ObDereferenceObject**を通じて) これらのオブジェクトへの参照を解放し、完了時に ( **exfreepool**を介して) リストを含むメモリを解放する必要があります。

この関数コードは、IRQL &lt;= ディスパッチ\_レベルで呼び出すことができます。

### <a name="see-also"></a>参照

[**Avc\_MULTIFUNC\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_multifunc_irb)、 [**avc\_ピア\_DO\_LIST**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_peer_do_list)、 [**avc\_関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)、[**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)、 [**ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)、 [**exfreepool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)

 

 





