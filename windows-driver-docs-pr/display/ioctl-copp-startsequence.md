---
title: IOCTL\_COPP\_StartSequence 制御コード
description: 現在のビデオ セッションを保護モードに設定します。
ms.assetid: a28e22d0-b54d-45d2-b32c-b0d96960a8a2
keywords:
- IOCTL_COPP_StartSequence 制御コード ディスプレイ デバイス
topic_type:
- apiref
api_name:
- IOCTL_COPP_StartSequence
api_type:
- NA
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: b502944c1d3a1926073a0d17db0027f5c04a3db1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386248"
---
# <a name="ioctlcoppstartsequence-control-code"></a>IOCTL\_COPP\_StartSequence 制御コード


現在のビデオ セッションを保護モードに設定します。

## <span id="ddk_ioctl_copp_startsequence_gg"></span><span id="DDK_IOCTL_COPP_STARTSEQUENCE_GG"></span>


### <a name="span-idinputparametersspanspan-idinputparametersspanspan-idinputparametersspaninput-parameters"></a><span id="Input_Parameters"></span><span id="input_parameters"></span><span id="INPUT_PARAMETERS"></span>入力パラメーター

[**ビデオ\_要求\_パケット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_request_packet) (VRP) **InputBuffer**ディスプレイ ドライバーから渡された情報が含まれています。 ディスプレイ ドライバーが、COPP にポインターを渡すことができます、\_IO\_InputBuffer 構造体の次のように定義されています。

```cpp
typedef struct {
    PVOID* ppThis;
    PVOID InputBuffer;
    HRESULT phr;
} COPP_IO_InputBuffer;
```

**PpThis**保護モードに設定されている COPP DirectX VA デバイス オブジェクトへのポインターへのポインターします。 **InputBuffer**メンバーへのポインターに設定されます、 [ **DXVA\_COPPSignature** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_coppsignature)保護されたセッションを開始する構造体。 **Phr**メンバーから返される値に設定する必要があります、 [ *COPPSequenceStart* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppsequencestart)関数。

### <a name="span-idoutputparametersspanspan-idoutputparametersspanspan-idoutputparametersspanoutput-parameters"></a><span id="Output_Parameters"></span><span id="output_parameters"></span><span id="OUTPUT_PARAMETERS"></span>出力パラメーター

なし

### <a name="span-idiostatusblockspanspan-idiostatusblockspanspan-idiostatusblockspanio-status-block"></a><span id="I_O_Status_Block"></span><span id="i_o_status_block"></span><span id="I_O_STATUS_BLOCK"></span>状態の I/O ブロック

ミニポート ドライバーが設定されていない、**情報**のメンバー、 [**状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_status_block)構造体。

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


[*COPPSequenceStart*](https://docs.microsoft.com/windows-hardware/drivers/display/coppsequencestart)

[**DXVA\_COPPSignature**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_coppsignature)

 

 






