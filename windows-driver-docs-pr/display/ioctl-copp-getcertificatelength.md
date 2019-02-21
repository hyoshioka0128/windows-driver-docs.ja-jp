---
title: IOCTL\_COPP\_GetCertificateLength 制御コード
description: グラフィックス ハードウェアで使用される証明書のバイト単位のサイズを返します。
ms.assetid: a65d301a-4b33-45f9-b21e-a2606d752b12
keywords:
- IOCTL_COPP_GetCertificateLength 制御コード ディスプレイ デバイス
topic_type:
- apiref
api_name:
- IOCTL_COPP_GetCertificateLength
api_type:
- NA
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 61d285558fe8cd8fd30eebb5d5aa8f330a3119f3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558794"
---
# <a name="ioctlcoppgetcertificatelength-control-code"></a>IOCTL\_COPP\_GetCertificateLength 制御コード


グラフィックス ハードウェアで使用される証明書のバイト単位のサイズを返します。

## <span id="ddk_ioctl_copp_getcertificatelength_gg"></span><span id="DDK_IOCTL_COPP_GETCERTIFICATELENGTH_GG"></span>


### <a name="span-idinputparametersspanspan-idinputparametersspanspan-idinputparametersspaninput-parameters"></a><span id="Input_Parameters"></span><span id="input_parameters"></span><span id="INPUT_PARAMETERS"></span>入力パラメーター

[**ビデオ\_要求\_パケット**](https://msdn.microsoft.com/library/windows/hardware/ff570547) (VRP) **InputBuffer**ディスプレイ ドライバーから渡された情報が含まれています。 ディスプレイ ドライバーが、COPP にポインターを渡すことができます、\_IO\_InputBuffer 構造体の次のように定義されています。

```cpp
typedef struct {
    PVOID* ppThis;
    PVOID InputBuffer;
    HRESULT phr;
} COPP_IO_InputBuffer;
```

**PpThis**ハードウェア証明書のサイズを取得するために使用する COPP DirectX VA デバイス オブジェクトへのポインターへのポインターします。 **InputBuffer**メンバーは必要ありません。 **Phr**メンバーから返される値に設定する必要があります、 [ *COPPGetCertificateLength* ](https://msdn.microsoft.com/library/windows/hardware/ff539644)関数。

### <a name="span-idoutputparametersspanspan-idoutputparametersspanspan-idoutputparametersspanoutput-parameters"></a><span id="Output_Parameters"></span><span id="output_parameters"></span><span id="OUTPUT_PARAMETERS"></span>出力パラメーター

ミニポート ドライバーが、VRP ULONG に型指定された変数へのポインターを返します**OutputBuffer**します。 変数は、ハードウェアの証明書のサイズを保持します。

### <a name="span-idiostatusblockspanspan-idiostatusblockspanspan-idiostatusblockspanio-status-block"></a><span id="I_O_Status_Block"></span><span id="i_o_status_block"></span><span id="I_O_STATUS_BLOCK"></span>状態の I/O ブロック

ミニポート ドライバーのセット、**情報**のメンバー、 [**状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff569732) sizeof(ULONG) 構造体。

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


[*COPPGetCertificateLength*](https://msdn.microsoft.com/library/windows/hardware/ff539644)

 

 






