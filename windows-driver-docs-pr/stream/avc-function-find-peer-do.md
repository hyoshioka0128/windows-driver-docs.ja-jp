---
title: AVC\_関数\_検索\_ピア\_の操作を行います
description: AVC\_関数\_検索\_ピア\_の操作を行います
ms.assetid: a21dde69-f005-4782-97d9-095a57b2b1a5
keywords:
- AVC_FUNCTION_FIND_PEER_DO ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- AVC_FUNCTION_FIND_PEER_DO
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1fee2d0e0c39508038a39cabc28e1f63e80eaf6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386747"
---
# <a name="avcfunctionfindpeerdo"></a>AVC\_関数\_検索\_ピア\_の操作を行います


## <span id="ddk_avc_function_find_peer_do_ks"></span><span id="DDK_AVC_FUNCTION_FIND_PEER_DO_KS"></span>


**AVC\_関数\_検索\_ピア\_は**関数コードでは、非仮想検索*avc.sys*インスタンス。

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
<td><p>STATUS_UNSUCCESSFUL</p></td>
<td><p>非仮想インスタンス<em>avc.sys</em>が見つかりませんでした</p></td>
</tr>
<tr class="even">
<td><p>STATUS_INVALID_GENERATION</p></td>
<td><p>デバイス オブジェクトの参照が見つかりませんでした前に、バスのリセットが発生しました。 新しい NodeAddress を取得し、もう一度やり直してください。</p></td>
</tr>
</tbody>
</table>

 

### <a name="comments"></a>コメント

この関数を使用して、 **PeerLocator** 、AVC のメンバー\_MULTIFUNC\_IRB 構造の下に示すようにします。

```cpp
typedef struct _AVC_MULTIFUNC_IRB {
  AVC_IRB  Common;
  union {
    .
    .
    .
    AVC_PEER_DO_LOCATOR PeerLocator;
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
**関数**にこのメンバーのサブメンバーを設定する必要があります**AVC\_関数\_検索\_ピア\_は**、AVC から\_関数列挙体です。

<span id="PeerLocator"></span><span id="peerlocator"></span><span id="PEERLOCATOR"></span>**PeerLocator**  
非仮想 (ピア) のインスタンスを指定します*avc.sys*します。

この関数では、非仮想検索*avc.sys*インスタンスに従ってデバイスのノードのアドレスに表します。 IRP がのステータスを完了すると、インスタンスが見つからない場合\_失敗しました。 インスタンスが配置されていると、呼び出し元がどの GUID を送信できます\_AVC\_クラス デバイスのインターフェイスを要求オブジェクトを使用します。 呼び出し元がこのオブジェクトへの参照を解放する必要があります (を通じて**ObDereferenceObject**) 作業を完了するとします。

この関数のコードは、IRQL で呼び出すことができます&lt;= ディスパッチ\_レベル。

### <a name="see-also"></a>関連項目

[**AVC\_MULTIFUNC\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avc_multifunc_irb), [**AVC\_PEER\_DO\_LOCATOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avc_peer_do_locator), [**AVC\_FUNCTION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ne-avc-_tagavc_function), [**ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject)

 

 





