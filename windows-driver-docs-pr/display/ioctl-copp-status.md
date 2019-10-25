---
title: IOCTL\_COPP\_ステータスコントロールコード
description: 保護されたビデオセッションの状態を返します。
ms.assetid: 58c841f6-0bc8-4c21-9c0e-fd409817ec91
keywords:
- IOCTL_COPP_Status コントロールのコード表示デバイス
topic_type:
- apiref
api_name:
- IOCTL_COPP_Status
api_type:
- NA
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: e182a03233dc89ee7629cf17d9ee083816590a55
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840333"
---
# <a name="ioctl_copp_status-control-code"></a>IOCTL\_COPP\_ステータスコントロールコード


保護されたビデオセッションの状態を返します。

## <span id="ddk_ioctl_copp_status_gg"></span><span id="DDK_IOCTL_COPP_STATUS_GG"></span>


### <a name="span-idinput_parametersspanspan-idinput_parametersspanspan-idinput_parametersspaninput-parameters"></a><span id="Input_Parameters"></span><span id="input_parameters"></span><span id="INPUT_PARAMETERS"></span>入力パラメーター

[**VIDEO\_REQUEST\_PACKET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_request_packet) (VRP) **InputBuffer**には、表示ドライバーから渡された情報が含まれています。 たとえば、表示ドライバーは、次のように定義されている COPP\_IO\_InputBuffer 構造体へのポインターを渡すことができます。

```cpp
typedef struct {
    PVOID* ppThis;
    PVOID InputBuffer;
    HRESULT phr;
} COPP_IO_InputBuffer;
```

**この**メンバーは、状態が取得される Copp DirectX VA デバイスオブジェクトへのポインターを指しています。 **InputBuffer**メンバーは、copp status 要求に関する情報を含む[**DXVA\_COPPStatusInput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusinput)構造体へのポインターに設定されます。 **Phr**メンバーは、 [*COPPQueryStatus*](https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus)関数から返された値に設定する必要があります。

### <a name="span-idoutput_parametersspanspan-idoutput_parametersspanspan-idoutput_parametersspanoutput-parameters"></a><span id="Output_Parameters"></span><span id="output_parameters"></span><span id="OUTPUT_PARAMETERS"></span>出力パラメーター

ミニポートドライバーは、VRP **Outputbuffer**内の[**DXVA\_COPPStatusOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusoutput)構造体へのポインターを返します。 DXVA\_COPPStatusOutput 構造体には、状態が含まれます。

### <a name="span-idi_o_status_blockspanspan-idi_o_status_blockspanspan-idi_o_status_blockspanio-status-block"></a><span id="I_O_Status_Block"></span><span id="i_o_status_block"></span><span id="I_O_STATUS_BLOCK"></span>I/o 状態ブロック

ミニポートドライバーは、[**状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_status_block)構造の**情報**メンバーを Sizeof (DXVA\_coppstatusoutput) に設定します。

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
<td align="left"><p>このセクションは、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。</p></td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[*COPPQueryStatus*](https://docs.microsoft.com/windows-hardware/drivers/display/coppquerystatus)

[**DXVA\_COPPStatusInput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusinput)

[**DXVA\_COPPStatusOutput**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_coppstatusoutput)

 

 






