---
title: AVC\_関数\_取得\_サブユニット\_情報
description: AVC\_関数\_取得\_サブユニット\_情報
ms.assetid: 1793df9d-b186-425f-a3dd-3054cb9b74bf
keywords:
- AVC_FUNCTION_GET_SUBUNIT_INFO ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- AVC_FUNCTION_GET_SUBUNIT_INFO
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6a4f3ce3ec7b4abb5f55488492a64d4ab77b1cc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358995"
---
# <a name="avcfunctiongetsubunitinfo"></a>AVC\_関数\_取得\_サブユニット\_情報


## <span id="ddk_avc_function_get_subunit_info_ks"></span><span id="DDK_AVC_FUNCTION_GET_SUBUNIT_INFO_KS"></span>


**AVC\_関数\_取得\_サブユニット\_情報**関数のコードは、ターゲット デバイスのサブユニット情報を取得します。

### <a name="io-status-block"></a>I/O ステータス ブロック

この関数は常に設定**Irp -&gt;IoStatus.Status**ステータス\_成功します。

### <a name="comments"></a>コメント

この関数を使用して、**サブユニット**、AVC のメンバー\_MULTIFUNC\_IRB 構造の下に示すようにします。

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

**ヘッダー:** 宣言されている*avc.h*します。 含める*avc.h*します。

### <a name="avcmultifuncirb-input"></a>AVC\_MULTIFUNC\_IRB 入力

**一般的です**  
**関数**にこのメンバーのサブメンバーを設定する必要があります**AVC\_関数\_取得\_サブユニット\_情報**、AVC から\_関数列挙体です。

<span id="Subunits"></span><span id="subunits"></span><span id="SUBUNITS"></span>**サブユニット**  
AV/C サブユニットの情報の説明を指定します。

この関数は、コマンドは、ターゲットに送信されませんので、ローカルで満たされます。

この関数のコードは、IRQL で呼び出すことができます&lt;= ディスパッチ\_レベル。

### <a name="see-also"></a>関連項目

[**AVC\_MULTIFUNC\_IRB**](https://msdn.microsoft.com/library/windows/hardware/ff554177), [**AVC\_SUBUNIT\_INFO\_BLOCK**](https://msdn.microsoft.com/library/windows/hardware/ff554199), [**AVC\_FUNCTION**](https://msdn.microsoft.com/library/windows/hardware/ff554145)

 

 





