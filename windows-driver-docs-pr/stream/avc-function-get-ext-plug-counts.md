---
title: AVC\_関数\_取得\_EXT\_プラグ\_カウント
description: AVC\_関数\_取得\_EXT\_プラグ\_カウント
ms.assetid: dced18ac-dc26-4c47-bc92-a3f3daec505b
keywords:
- AVC_FUNCTION_GET_EXT_PLUG_COUNTS ストリーミング メディア デバイス
topic_type:
- apiref
api_name:
- AVC_FUNCTION_GET_EXT_PLUG_COUNTS
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65fe4cde47b5526f4326e1fd4b82e10d74546398
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386744"
---
# <a name="avcfunctiongetextplugcounts"></a>AVC\_関数\_取得\_EXT\_プラグ\_カウント


## <span id="ddk_avc_function_get_ext_plug_counts_ks"></span><span id="DDK_AVC_FUNCTION_GET_EXT_PLUG_COUNTS_KS"></span>


**AVC\_関数\_取得\_EXT\_プラグイン\_カウント**関数コードが外部入力を取得し、出力プラグインの数。

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

この関数を使用して、 **ExtPlugCounts** 、AVC のメンバー\_MULTIFUNC\_IRB 構造の下に示すようにします。

```cpp
typedef struct _AVC_MULTIFUNC_IRB {
  AVC_IRB  Common;
  union {
    .
    .
    .
    AVC_EXT_PLUG_COUNTS ExtPlugCounts;
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
**関数**にこのメンバーのサブメンバーを設定する必要があります**AVC\_関数\_取得\_EXT\_プラグ\_カウント**AVCから\_関数の列挙体です。

<span id="ExtPlugCounts"></span><span id="extplugcounts"></span><span id="EXTPLUGCOUNTS"></span>**ExtPlugCounts**  
外部入力と出力プラグの数を指定します。

仮想インスタンスでは、この関数のコードはサポートされていない*avc.sys*します。

サブユニット ドライバーは、関数、形式、および外部プラグインするときの使用を決定する責任を負います。 *Avc.sys*専用ピンとサブユニットにプラグインするときに外部とのサブユニット プラグの間で永続的な接続を報告は、ただし、(詳細については、次を参照してください[ **AVC\_関数\_GET。\_接続情報**](avc-function-get-connectinfo.md))。

これは、IRQL で呼び出す必要がある = パッシブ\_レベル。

### <a name="see-also"></a>関連項目

[**AVC\_MULTIFUNC\_IRB**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avc_multifunc_irb), [**AVC\_EXT\_PLUG\_COUNTS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ns-avc-_avc_ext_plug_counts), [**AVC\_FUNCTION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/avc/ne-avc-_tagavc_function)

 

 





