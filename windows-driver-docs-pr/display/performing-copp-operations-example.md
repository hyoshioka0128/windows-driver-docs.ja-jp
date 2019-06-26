---
title: COPP 操作の実行例
description: COPP 演算を実行する例
ms.assetid: ba5c98d3-63d1-4e2d-ba11-6054c1623e80
keywords:
- 保護 WDK COPP、COPP 操作のコード例をコピーします。
- ビデオのコピー防止 WDK COPP、COPP 操作のコード例
- COPP WDK DirectX va なので、操作のコード例
- ビデオの WDK COPP COPP 操作の例のコードの保護
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f5954313b6994309e2a56d1e80ab7bde6204bae
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385581"
---
# <a name="performing-copp-operations-example"></a>COPP 操作の実行例


## <span id="ddk_performing_copp_operations_gg"></span><span id="DDK_PERFORMING_COPP_OPERATIONS_GG"></span>


**このセクションには、Windows Server 2003 SP1 にのみ以降が適用されますおよび Windows XP SP2 以降。**

経由で、認定出力保護プロトコル (COPP) 操作を実行するのにには、次のコード例を使用します。 コード例の実装、 [ *DdMoCompRender* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)コールバック関数。 **RenderMoComp**のメンバー、 [ **DD\_MOTIONCOMPCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)コールバック関数へのポインターを構造体します。 この例のコードのみは*DdMoCompRender* COPP 操作のために使用します。 実装について*DdMoCompRender* ProcAmp コントロールを実行して、操作をデインター レースを参照してください[ProcAmp コントロールを実行して操作のデインター レース](performing-procamp-control-and-deinterlacing-operations.md)と[実行サブストリーム合成の操作でデインター レース](performing-deinterlacing-with-substream-compositing-operations.md)します。

```cpp
DWORD APIENTRY
  MOCOMPCB_RENDER(
    PDD_RENDERMOCOMPDATA  lpData
    )
{
    // The driver saves the device class object in lpDriverReserved1 
     // during the DdMoCompCreate callback. For more information, 
     // see Creating Instances of DirectX VA Device Objects.
  DXVA_DeviceBaseClass* pDXVABase =
         (DXVA_DeviceBaseClass*)lpData->lpMoComp->lpDriverReserved1;
 if (pDXVABase == NULL) {
        lpData->ddRVal = E_POINTER;
        return DDHAL_DRIVER_HANDLED;
    }
    // Process according to the device type in the class object.
     // For more information, see Defining DirectX VA Device Classes.
    switch (pDXVABase->m_DeviceType) {
    // This is the COPP device.
    case DXVA_DeviceCOPP:
        {
            DXVA_COPPDeviceClass* pDXVACopp =
                        (DXVA_COPPDeviceClass*)pDXVABase;
            ULONG BytesReturned;
            HANDLE handle = (HANDLE)GetDriverHandleFromPDEV(lpData->lpDD->lpGbl->dhpdev)
            COPP_IO_InputBuffer InputBuffer;
            InputBuffer.ppThis = &pDXVACopp->m_pThis;
            InputBuffer.phr = &lpData->ddRVal;
            switch (lpData->dwFunction) {
            case DXVA_COPPGetCertificateLengthFnCode:
                if (lpData->dwOutputDataSize < sizeof(ULONG)) {
 lpData->ddRVal = E_INVALIDARG;
                }
                else { 
 InputBuffer.InputBuffer = NULL;
                    EngDeviceIoControl(handle,
                                      IOCTL_COPP_GetCertificateLength,
                                      &InputBuffer,
                                      sizeof(InputBuffer),
                                      lpData->lpOutputData,
                                      lpData->dwOutputDataSize,
                                      &BytesReturned);
                }
                break;
            case DXVA_COPPKeyExchangeFnCode:
                if (lpData->dwOutputDataSize < sizeof(DXVA_COPPKeyExchangeOutput)) {
  lpData->ddRVal = E_INVALIDARG;
                }
                else {
 InputBuffer.InputBuffer = NULL;
                    DD_SURFACE_LOCAL* lpCompSurf =
                        lpData->lpBufferInfo[0].lpCompSurface;
                    InputBuffer.InputBuffer = (PVOID)lpCompSurf->lpGbl->fpVidMem;
                    EngDeviceIoControl(handle
                                       IOCTL_COPP_KeyExchange,
                                       &InputBuffer,
                                        sizeof(InputBuffer),
                                       lpData->lpOutputData,
                                       lpData->dwOutputDataSize,
                                       &BytesReturned);
                }
                break;
            case DXVA_COPPSequenceStartFnCode:
                if (lpData->dwInputDataSize < sizeof(DXVA_COPPSignature)) {
 lpData->ddRVal = E_INVALIDARG;
                }
                else {
                    InputBuffer.InputBuffer = lpData->lpInputData;
                    EngDeviceIoControl(handle,
 IOCTL_COPP_StartSequence,
                                       &InputBuffer,
                                       sizeof(InputBuffer),
                                       NULL,
                                       0,
                                       &BytesReturned);
                }
                break;
            case DXVA_COPPCommandFnCode:
                if (lpData->dwInputDataSize < sizeof(DXVA_COPPCommand)) {
 lpData->ddRVal = E_INVALIDARG;
                }
                else {
                    InputBuffer.InputBuffer = lpData->lpInputData;
                    EngDeviceIoControl(handle,
 IOCTL_COPP_Command,
                                       &InputBuffer,
                                       sizeof(InputBuffer),
                                       NULL,
                                       0,
                                       &BytesReturned);
                }
                break;
            case DXVA_COPPQueryStatusFnCode:
                if (lpData->dwInputDataSize < sizeof(DXVA_COPPStatusInput) ||
                    lpData->dwOutputDataSize < sizeof(DXVA_COPPStatusOutput)) {
 lpData->ddRVal = E_INVALIDARG;
                }
                else {
                    InputBuffer.InputBuffer = lpData->lpInputData;
                    EngDeviceIoControl(handle,
 IOCTL_COPP_Status,
                                       &InputBuffer,
                                       sizeof(InputBuffer),
                                       lpData->lpOutputData,
                                       lpData->dwOutputDataSize,
                                       &BytesReturned);
 }
                break;
            default:
                lpData->ddRVal = E_INVALIDARG;
 break;
            }
            break;
        }
    }
    return DDHAL_DRIVER_HANDLED;
}
```

 

 





