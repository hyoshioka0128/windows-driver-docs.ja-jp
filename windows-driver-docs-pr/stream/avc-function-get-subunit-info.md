---
title: AVC\_関数\_\_サブユニット\_情報を取得します
description: AVC\_関数\_\_サブユニット\_情報を取得します
ms.assetid: 1793df9d-b186-425f-a3dd-3054cb9b74bf
keywords:
- AVC_FUNCTION_GET_SUBUNIT_INFO ストリーミングメディアデバイス
topic_type:
- apiref
api_name:
- AVC_FUNCTION_GET_SUBUNIT_INFO
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: aba7def57219a1e799dafdda71b4cfd1181deca5
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845079"
---
# <a name="avc_function_get_subunit_info"></a>AVC\_関数\_\_サブユニット\_情報を取得します


## <span id="ddk_avc_function_get_subunit_info_ks"></span><span id="DDK_AVC_FUNCTION_GET_SUBUNIT_INFO_KS"></span>


**AVC\_関数\_取得\_サブユニット\_情報**関数コードは、ターゲットデバイスのサブユニット情報を取得します。

### <a name="io-status-block"></a>I/O ステータス ブロック

この関数は常に **、Irp&gt;iostatus. status**を STATUS\_SUCCESS に設定します。

### <a name="comments"></a>コメント

この関数は、次に示すように、AVC\_MULTIFUNC\_IRB 構造体の**サブユニット**メンバーを使用します。

```cpp
typedef struct _AVC_MULTIFUNC_IRB {
  AVC_IRB  Common;
  union {
    .
    .
    .
    AVC_SUBUNIT_INFO_BLOCK Subunits;
 };
} AVC_MULTIFUNC_IRB, *PAVC_MULTIFUNC_IRB;
```

### <a name="requirements"></a>要件

**ヘッダー:** *Avc*で宣言されています。 *Avc. h*を含めます。

### <a name="avc_multifunc_irb-input"></a>AVC\_MULTIFUNC\_IRB 入力

**的**  
このメンバーの**関数**submember は、AVC\_関数の列挙から **\_サブユニット\_情報を取得\_には、avc\_関数**に設定する必要があります。

<span id="Subunits"></span><span id="subunits"></span><span id="SUBUNITS"></span>**サブユニット**  
AV/C サブユニットの情報の説明を指定します。

この関数はローカルで満たされているため、ターゲットにコマンドは送信されません。

この関数コードは、IRQL &lt;= ディスパッチ\_レベルで呼び出すことができます。

### <a name="see-also"></a>参照

[**Avc\_MULTIFUNC\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_multifunc_irb)、 [**AVC\_サブユニット\_INFO\_BLOCK**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ns-avc-_avc_subunit_info_block)、 [**AVC\_関数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/avc/ne-avc-_tagavc_function)

 

 





