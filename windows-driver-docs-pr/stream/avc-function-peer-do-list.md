---
title: AVC\_関数\_ピア\_は\_一覧
description: AVC\_関数\_ピア\_は\_一覧
ms.assetid: 80ffd94e-788f-4874-b716-3eb66d90e4aa
keywords:
- AVC_FUNCTION_PEER_DO_LIST ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- AVC_FUNCTION_PEER_DO_LIST
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fcf8bff68757c53652db812fa93de5641e977be
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386726"
---
# <a name="avcfunctionpeerdolist"></a>AVC\_関数\_ピア\_は\_一覧


## <span id="ddk_avc_function_peer_do_list_ks"></span><span id="DDK_AVC_FUNCTION_PEER_DO_LIST_KS"></span>


**AVC\_関数\_ピア\_は\_一覧**すべて非仮想関数のコードでは検索*avc.sys*インスタンス。

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
<td><p>STATUS_INSUFFICIENT_RESOURCES</p></td>
<td><p>デバイス オブジェクトの参照の一覧については、領域を取得できませんでした。</p></td>
</tr>
</tbody>
</table>

 

### <a name="comments"></a>コメント

この関数を使用して、**よう**、AVC のメンバー\_MULTIFUNC\_IRB 構造の下に示すようにします。

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

**ヘッダー:** 宣言されている*avc.h*します。 含める*avc.h*します。

### <a name="avcmultifuncirb-input"></a>AVC\_MULTIFUNC\_IRB 入力

**一般的です**  
**関数**にこのメンバーのサブメンバーを設定する必要があります**AVC\_関数\_ピア\_は\_一覧**、AVC から\_関数列挙体です。

<span id="PeerList"></span><span id="peerlist"></span><span id="PEERLIST"></span>**よう**  
すべての非仮想 (ピア) インスタンスの一覧を示す*avc.sys*します。

呼び出し元が送信した GUID\_AVC\_クラス デバイス インターフェイスの要求を任意のオブジェクトがオブジェクトの一覧で返されます。 呼び出し元は、これらのオブジェクトへの参照を解放する必要があります (を通じて**ObDereferenceObject**)、し、一覧を格納しているメモリを解放 (を通じて**ExFreePool**) が完了します。

この関数のコードは、IRQL で呼び出すことができます&lt;= ディスパッチ\_レベル。

### <a name="see-also"></a>関連項目

[**AVC\_MULTIFUNC\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avc_multifunc_irb)、 [ **AVC\_ピア\_は\_一覧**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avc_peer_do_list)、 [ **AVC\_関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ne-avc-_tagavc_function)、 [**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_object)、 [ **ObDereferenceObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject)、 [ **ExFreePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool)

 

 





