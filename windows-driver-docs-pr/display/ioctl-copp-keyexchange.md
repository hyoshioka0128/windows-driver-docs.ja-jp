---
title: IOCTL\_COPP\_KeyExchange 制御コード
description: グラフィックスハードウェアによって使用されるデジタル証明書を返します。
ms.assetid: edb0d4db-cf7e-4e13-a25b-8fce0e9f2ec0
keywords:
- IOCTL_COPP_KeyExchange コントロールのコード表示デバイス
topic_type:
- apiref
api_name:
- IOCTL_COPP_KeyExchange
api_type:
- NA
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: c709840776e02f713e0e6f1134ea03cca6a5156a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840335"
---
# <a name="ioctl_copp_keyexchange-control-code"></a>IOCTL\_COPP\_KeyExchange 制御コード


グラフィックスハードウェアによって使用されるデジタル証明書を返します。

## <span id="ddk_ioctl_copp_keyexchange_gg"></span><span id="DDK_IOCTL_COPP_KEYEXCHANGE_GG"></span>


### <a name="span-idinput_parametersspanspan-idinput_parametersspanspan-idinput_parametersspaninput-parameters"></a><span id="Input_Parameters"></span><span id="input_parameters"></span><span id="INPUT_PARAMETERS"></span>入力パラメーター

[**VIDEO\_REQUEST\_PACKET**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_request_packet) (VRP) **InputBuffer**には、表示ドライバーから渡された情報が含まれています。 たとえば、表示ドライバーは、次のように定義されている COPP\_IO\_InputBuffer 構造体へのポインターを渡すことができます。

```cpp
typedef struct {
    PVOID* ppThis;
    PVOID InputBuffer;
    HRESULT phr;
} COPP_IO_InputBuffer;
```

**この**メンバーは、ハードウェアデジタル証明書を取得するために使用される、Copp DirectX VA デバイスオブジェクトへのポインターを指しています。 **InputBuffer**メンバーは必要ありません。 **Phr**メンバーは、 [*COPPKeyExchange*](https://docs.microsoft.com/windows-hardware/drivers/display/coppkeyexchange)関数から返された値に設定する必要があります。

### <a name="span-idoutput_parametersspanspan-idoutput_parametersspanspan-idoutput_parametersspanoutput-parameters"></a><span id="Output_Parameters"></span><span id="output_parameters"></span><span id="OUTPUT_PARAMETERS"></span>出力パラメーター

ミニポートドライバーは、VRP **Outputbuffer**内のバイト配列を返します。 この配列には、デジタル証明書が含まれています。

### <a name="span-idi_o_status_blockspanspan-idi_o_status_blockspanspan-idi_o_status_blockspanio-status-block"></a><span id="I_O_Status_Block"></span><span id="i_o_status_block"></span><span id="I_O_STATUS_BLOCK"></span>I/o 状態ブロック

ミニポートドライバーは、[**状態\_ブロック**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_status_block)構造の**情報**メンバーを、VRP の**outputbufferlength**メンバーの値に設定します。

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


[*COPPKeyExchange*](https://docs.microsoft.com/windows-hardware/drivers/display/coppkeyexchange)

 

 






