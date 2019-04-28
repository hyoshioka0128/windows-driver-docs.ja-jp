---
title: IOCTL\_COPP\_KeyExchange 制御コード
description: グラフィックス ハードウェアで使用されるデジタル証明書を返します。
ms.assetid: edb0d4db-cf7e-4e13-a25b-8fce0e9f2ec0
keywords:
- IOCTL_COPP_KeyExchange 制御コード ディスプレイ デバイス
topic_type:
- apiref
api_name:
- IOCTL_COPP_KeyExchange
api_type:
- NA
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7341d7a7c324635ee518c776b772f6b55ca446db
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362102"
---
# <a name="ioctlcoppkeyexchange-control-code"></a>IOCTL\_COPP\_KeyExchange 制御コード


グラフィックス ハードウェアで使用されるデジタル証明書を返します。

## <span id="ddk_ioctl_copp_keyexchange_gg"></span><span id="DDK_IOCTL_COPP_KEYEXCHANGE_GG"></span>


### <a name="span-idinputparametersspanspan-idinputparametersspanspan-idinputparametersspaninput-parameters"></a><span id="Input_Parameters"></span><span id="input_parameters"></span><span id="INPUT_PARAMETERS"></span>入力パラメーター

[**ビデオ\_要求\_パケット**](https://msdn.microsoft.com/library/windows/hardware/ff570547) (VRP) **InputBuffer**ディスプレイ ドライバーから渡された情報が含まれています。 ディスプレイ ドライバーが、COPP にポインターを渡すことができます、\_IO\_InputBuffer 構造体の次のように定義されています。

```cpp
typedef struct {
    PVOID* ppThis;
    PVOID InputBuffer;
    HRESULT phr;
} COPP_IO_InputBuffer;
```

**PpThis**ハードウェアのデジタル証明書を取得するために使用する COPP DirectX VA デバイス オブジェクトへのポインターへのポインターします。 **InputBuffer**メンバーは必要ありません。 **Phr**メンバーから返される値に設定する必要があります、 [ *COPPKeyExchange* ](https://msdn.microsoft.com/library/windows/hardware/ff539646)関数。

### <a name="span-idoutputparametersspanspan-idoutputparametersspanspan-idoutputparametersspanoutput-parameters"></a><span id="Output_Parameters"></span><span id="output_parameters"></span><span id="OUTPUT_PARAMETERS"></span>出力パラメーター

ミニポート ドライバーでは、バイトの配列を返します、VRP で**OutputBuffer**します。 配列には、デジタル証明書が含まれています。

### <a name="span-idiostatusblockspanspan-idiostatusblockspanspan-idiostatusblockspanio-status-block"></a><span id="I_O_Status_Block"></span><span id="i_o_status_block"></span><span id="I_O_STATUS_BLOCK"></span>状態の I/O ブロック

ミニポート ドライバーのセット、**情報**のメンバー、 [**状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff569732)構造体の値を**OutputBufferLength** 、VRP のメンバー。

<a name="requirements"></a>要件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>バージョン</p></td>
<td align="left"><p>このセクションでは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。</p></td>
</tr>
</tbody>
</table>

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[*COPPKeyExchange*](https://msdn.microsoft.com/library/windows/hardware/ff539646)

 

 






