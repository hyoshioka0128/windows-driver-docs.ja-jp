---
title: IOCTL\_COPP\_コマンド コントロール コード
description: COPP DirectX VA デバイスで操作を実行します。
ms.assetid: 8593da3d-8e94-4820-91ce-92eb6d624a40
keywords:
- IOCTL_COPP_Command 制御コード ディスプレイ デバイス
topic_type:
- apiref
api_name:
- IOCTL_COPP_Command
api_type:
- NA
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7694942484945c32a60a115317283405d1621313
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372935"
---
# <a name="ioctlcoppcommand-control-code"></a>IOCTL\_COPP\_コマンド コントロール コード


COPP DirectX VA デバイスで操作を実行します。

## <span id="ddk_ioctl_copp_command_gg"></span><span id="DDK_IOCTL_COPP_COMMAND_GG"></span>


### <a name="span-idinputparametersspanspan-idinputparametersspanspan-idinputparametersspaninput-parameters"></a><span id="Input_Parameters"></span><span id="input_parameters"></span><span id="INPUT_PARAMETERS"></span>入力パラメーター

[**ビデオ\_要求\_パケット**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_request_packet) (VRP) **InputBuffer**ディスプレイ ドライバーから渡された情報が含まれています。 ディスプレイ ドライバーが、COPP にポインターを渡すことができます、\_IO\_InputBuffer 構造体の次のように定義されています。

```cpp
typedef struct {
    PVOID* ppThis;
    PVOID InputBuffer;
    HRESULT phr;
} COPP_IO_InputBuffer;
```

**PpThis** COPP DirectX VA デバイスへのポインターが指すメンバーが、操作が実行されるオブジェクトします。 **InputBuffer**メンバーへのポインターに設定されます、 [ **DXVA\_COPPCommand** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_coppcommand) COPP を記述する構造体のコマンドを実行します。 **Phr**メンバーから返される値に設定する必要があります、 [ *COPPCommand* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)関数。

### <a name="span-idoutputparametersspanspan-idoutputparametersspanspan-idoutputparametersspanoutput-parameters"></a><span id="Output_Parameters"></span><span id="output_parameters"></span><span id="OUTPUT_PARAMETERS"></span>出力パラメーター

なし

### <a name="span-idiostatusblockspanspan-idiostatusblockspanspan-idiostatusblockspanio-status-block"></a><span id="I_O_Status_Block"></span><span id="i_o_status_block"></span><span id="I_O_STATUS_BLOCK"></span>状態の I/O ブロック

ミニポート ドライバーが設定されていない、**情報**のメンバー、 [**状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_status_block)構造体。

<a name="requirements"></a>必要条件
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


[*COPPCommand*](https://docs.microsoft.com/windows-hardware/drivers/display/coppcommand)

[**DXVA\_COPPCommand**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_coppcommand)

 

 






