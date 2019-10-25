---
title: '\_PEER\_DO\_検索する AVC\_関数'
description: '\_PEER\_DO\_検索する AVC\_関数'
ms.assetid: a21dde69-f005-4782-97d9-095a57b2b1a5
keywords:
- AVC_FUNCTION_FIND_PEER_DO ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- AVC_FUNCTION_FIND_PEER_DO
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07c47c7665a154c4c404567403c3ad6768795056
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845159"
---
# <a name="avc_function_find_peer_do"></a>\_PEER\_DO\_検索する AVC\_関数


## <span id="ddk_avc_function_find_peer_do_ks"></span><span id="DDK_AVC_FUNCTION_FIND_PEER_DO_KS"></span>


**Avc\_関数\_FIND\_PEER\_DO**関数コードは、非仮想の*AVC*インスタンスを検索します。

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
<td><p>STATUS_UNSUCCESSFUL</p></td>
<td><p><em>Avc</em>の非仮想インスタンスが見つかりませんでした</p></td>
</tr>
<tr class="even">
<td><p>STATUS_INVALID_GENERATION</p></td>
<td><p>バスリセットが発生したため、デバイスオブジェクト参照が見つかりませんでした。 新しい NodeAddress を取得して、もう一度やり直してください。</p></td>
</tr>
</tbody>
</table>

 

### <a name="comments"></a>コメント

この関数は、次に示すように、AVC\_MULTIFUNC\_IRB 構造体の**Peerlocator**メンバーを使用します。

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

### <a name="requirements"></a>要件

**ヘッダー:** *Avc*で宣言されています。 *Avc. h*を含めます。

### <a name="avc_multifunc_irb-input"></a>AVC\_MULTIFUNC\_IRB 入力

**的**  
このメンバーの**関数**サブメンバーを AVC\_関数に設定して、AVC\_関数の列挙から **\_\_ピアを検索\_** 必要があります。

<span id="PeerLocator"></span><span id="peerlocator"></span><span id="PEERLOCATOR"></span>**PeerLocator**  
*Avc*の非仮想 (ピア) インスタンスを指定します。

この関数は、それが表すデバイスのノードアドレスに応じて、非仮想の*avc*インスタンスを検索します。 インスタンスが見つからない場合、IRP は状態\_[失敗] の状態で完了します。 インスタンスが見つかると、呼び出し元は、オブジェクトを介して、AVC\_クラスのデバイスインターフェイス要求\_任意の GUID を送信できます。 呼び出し元は、操作が完了したら、このオブジェクトへの参照を ( **ObDereferenceObject**を通じて) 解放する必要があります。

この関数コードは、IRQL &lt;= ディスパッチ\_レベルで呼び出すことができます。

### <a name="see-also"></a>参照

[**Avc\_MULTIFUNC\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_multifunc_irb)、 [**avc\_ピア\_DO\_LOCATOR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_peer_do_locator)、 [**avc\_関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)、 [**ObDereferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject)

 

 





