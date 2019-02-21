---
title: IOCTL\_COPP\_状態制御コード
description: 保護されたビデオ セッションの状態を返します。
ms.assetid: 58c841f6-0bc8-4c21-9c0e-fd409817ec91
keywords:
- IOCTL_COPP_Status は、コード ディスプレイ デバイスを制御します。
topic_type:
- apiref
api_name:
- IOCTL_COPP_Status
api_type:
- NA
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9f973c775a6f415838ec919d77e210c8ddafe1cf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536185"
---
# <a name="ioctlcoppstatus-control-code"></a>IOCTL\_COPP\_状態制御コード


保護されたビデオ セッションの状態を返します。

## <span id="ddk_ioctl_copp_status_gg"></span><span id="DDK_IOCTL_COPP_STATUS_GG"></span>


### <a name="span-idinputparametersspanspan-idinputparametersspanspan-idinputparametersspaninput-parameters"></a><span id="Input_Parameters"></span><span id="input_parameters"></span><span id="INPUT_PARAMETERS"></span>入力パラメーター

[**ビデオ\_要求\_パケット**](https://msdn.microsoft.com/library/windows/hardware/ff570547) (VRP) **InputBuffer**ディスプレイ ドライバーから渡された情報が含まれています。 ディスプレイ ドライバーが、COPP にポインターを渡すことができます、\_IO\_InputBuffer 構造体の次のように定義されています。

```cpp
typedef struct {
    PVOID* ppThis;
    PVOID InputBuffer;
    HRESULT phr;
} COPP_IO_InputBuffer;
```

**PpThis** COPP DirectX VA デバイス オブジェクトの状態を取得するへのポインターへのポインターします。 **InputBuffer**メンバーへのポインターに設定されます、 [ **DXVA\_COPPStatusInput** ](https://msdn.microsoft.com/library/windows/hardware/ff563899) COPP 状態要求に関する情報を含む構造体。 **Phr**メンバーから返される値に設定する必要があります、 [ *COPPQueryStatus* ](https://msdn.microsoft.com/library/windows/hardware/ff539652)関数。

### <a name="span-idoutputparametersspanspan-idoutputparametersspanspan-idoutputparametersspanoutput-parameters"></a><span id="Output_Parameters"></span><span id="output_parameters"></span><span id="OUTPUT_PARAMETERS"></span>出力パラメーター

ミニポート ドライバーへのポインターを返します、 [ **DXVA\_COPPStatusOutput** ](https://msdn.microsoft.com/library/windows/hardware/ff563903)構造、VRP **OutputBuffer**します。 DXVA\_COPPStatusOutput 構造体には、状態が含まれています。

### <a name="span-idiostatusblockspanspan-idiostatusblockspanspan-idiostatusblockspanio-status-block"></a><span id="I_O_Status_Block"></span><span id="i_o_status_block"></span><span id="I_O_STATUS_BLOCK"></span>状態の I/O ブロック

ミニポート ドライバーのセット、**情報**のメンバー、 [**状態\_ブロック**](https://msdn.microsoft.com/library/windows/hardware/ff569732) sizeof 構造体 (DXVA\_COPPStatusOutput)。

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


[*COPPQueryStatus*](https://msdn.microsoft.com/library/windows/hardware/ff539652)

[**DXVA\_COPPStatusInput**](https://msdn.microsoft.com/library/windows/hardware/ff563899)

[**DXVA\_COPPStatusOutput**](https://msdn.microsoft.com/library/windows/hardware/ff563903)

 

 






