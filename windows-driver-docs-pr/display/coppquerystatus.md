---
title: COPPQueryStatus 関数
description: COPPQueryStatus 関数のサンプルでは、COPP DirectX VA デバイスに関連付けられている保護されたビデオ セッションの状態を取得します。
ms.assetid: c2265df7-8b60-4a14-b7dc-ee227ad062dc
keywords:
- 保護 WDK COPP、ビデオのミニポート ドライバー コード テンプレートのコピーします。
- ビデオのコピー防止 WDK COPP、ビデオのミニポート ドライバー コード テンプレート
- 保護されたビデオ WDK COPP、ビデオのミニポート ドライバー コード テンプレート
- ビデオのミニポート ドライバー WDK Windows 2000、COPP コード テンプレート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab40601db1fdbeedf41b1dcc4c41e0fd2ffa6ad9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331350"
---
# <a name="coppquerystatus-function"></a>COPPQueryStatus 関数

COPPQueryStatus 関数のサンプルでは、COPP DirectX VA デバイスに関連付けられている保護されたビデオ セッションの状態を取得します。

### <a name="syntax"></a>構文

```cpp
HRESULT COPPQueryStatus(
  _In_  COPP_DeviceData       pThis,
  _In_  DXVA_COPPStatusInput  *pInput,
  _Out_ DXVA_COPPStatusOutput *pOutput
);
```

## <a name="parameters"></a>パラメーター

*[in] pThis*

* COPP DirectX VA デバイス オブジェクトへのポインター。

*[in] pInput*

* 特定のステータス情報を取得する要求を含む DXVA_COPPStatusInput 構造へのポインターを提供します。

*pOutput [out]*

* 使用している物理コネクタに関する状態情報を受け取る DXVA_COPPStatusOutput 構造体へのポインター。

## <a name="return-value"></a>戻り値

0 (S_OK または DD_OK) を返します成功した場合。それ以外の場合、エラー コードを返します。

## <a name="remarks"></a>注釈

ビデオのセッションは、保護モードに設定する必要があります (つまり、必要がある active) 関連付けられている COPP DirectX VA する前にデバイスがその COPPQueryStatus 関数の呼び出しを受信します。 つまり、COPPQueryStatus する前に、COPPSequenceStart 関数を呼び出す必要があります。 COPPQueryStatus は COPPSequenceStart する前に呼び出されると、COPPQueryStatus は E_UNEXPECTED を返します。

COPPQueryStatus 関数は、状態要求を含む pInput に設定されている DXVA_COPPStatusInput 構造体を受け取ります。 COPPQueryStatus 関数は、要求を処理し、pOutput で DXVA_COPPStatusOutput 構造内の適切な状態を返します。

## <a name="mapping-rendermocomp-to-coppquerystatus"></a>COPPQueryStatus へ RenderMoComp のマッピング

COPPQueryStatus 関数のサンプルは、DD_MOTIONCOMPCALLBACKS 構造体の RenderMoComp メンバーへの呼び出しに直接マップされます。 RenderMoComp メンバーは、ディスプレイ ドライバーによって提供される DdMoCompRender コールバックを参照する関数 DD_RENDERMOCOMPDATA 構造体を指します。

RenderMoComp のコールバック関数が関数を使用せず、ディスプレイ ドライバーによって提供される BeginMoCompFrame または EndMoCompFrame 最初に呼び出されると呼ばれます。

DD_RENDERMOCOMPDATA 構造は次のように入力されます。

|メンバー |値 | |dwNumBuffers |0 を返します。 | | lpBufferInfo | NULL. | |dwFunction |DXVA_COPPQueryStatusFnCode 定数が (dxva.h で定義されている)。 | |lpInputData |DXVA_COPPStatusInput 構造体へのポインター。 | |lpOutputData |DXVA_COPPStatusOutput 構造体へのポインター。 |

## <a name="example-code"></a>コードの例

次のコードでは、COPPQueryStatus 関数を実装する方法の例を示します。

```cpp
HRESULT
COPPQueryStatus(
    COPP_DeviceData* pThis,
    DXVA_COPPStatusInput* pStatusInput,
    DXVA_COPPStatusOutput* pStatusOutput
    )
{
    if (pThis->m_COPPDevState != COPP_SESSION_ACTIVE) {
        return E_UNEXPECTED;
    }
    if (pStatusInput->dwSequence != pThis->m_StatusSeqNumber) {
        return E_INVALIDARG;
    }
    //
    // reset the output buffer
    //
    memset(pStatusOutput, 0, sizeof(DXVA_COPPStatusOutput));
    if (IsEqualGUID(&DXVA_COPPQueryConnectorType, &pStatusInput->guidStatusRequestID)) {
        // Verify no input data for this status request.
        if (pStatusInput->cbSizeData != 0) {
            return E_INVALIDARG;
        }
        DXVA_COPPStatusData Tmp;
        Tmp.rApp = pStatusInput->rApp;
        Tmp.dwData = g_ConnectorInfo[pThis->m_DevID].ConnType;
        Tmp.dwFlags = COPP_StatusNormal;
        pStatusOutput->cbSizeData = sizeof(Tmp);
        memcpy(pStatusOutput->COPPStatus, &Tmp,sizeof(Tmp));
    }
    else if (IsEqualGUID(&DXVA_COPPQueryProtectionType, &pStatusInput->guidStatusRequestID)) {
        // verify that there is no input data for this status request
        if (pStatusInput->cbSizeData != 0) {
            return E_INVALIDARG;
        }
        DXVA_COPPStatusData Tmp;
        Tmp.rApp = pStatusInput->rApp;
        Tmp.dwData = g_ConnectorInfo[pThis->m_DevID].ProtectionTypeMask;
        Tmp.dwFlags = COPP_StatusNormal;
        pStatusOutput->cbSizeData = sizeof(Tmp);
        memcpy(pStatusOutput->COPPStatus, &Tmp,sizeof(Tmp));
    }
    else if (IsEqualGUID(&DXVA_COPPQueryLocalProtectionLevel, &pStatusInput->guidStatusRequestID) ||
             IsEqualGUID(&DXVA_COPPQueryGlobalProtectionLevel, &pStatusInput->guidStatusRequestID)) {
        DWORD ProtType;
        DWORD ProtIndex;
        DWORD Level;
        // verify that there is a single DWORD input data for this status request
        if (pStatusInput->cbSizeData != sizeof (DWORD)) {
            return E_INVALIDARG;
        }
        memcpy(&ProtType, (LPVOID)&pStatusInput->StatusData[0], sizeof(DWORD));
        // verify that no invalid protection type bits are set
        if (ProtType & ~COPP_ProtectionType_Mask) {
            return E_INVALIDARG;
        }
        // verify that only the protection level of a single protection type is requested
        ProtIndex = MapProtectionTypeToProtectionIndex(ProtType);
        if (ProtIndex == COPP_ProtectionTypeIndex_Unkonwn) {
            return E_INVALIDARG;
        }
        // verify that the video session supports the protection type
        if (!(g_ConnectorInfo[pThis->m_DevID].ProtectionTypeMask & ProtType)) {
            return E_INVALIDARG;
        }
        if (IsEqualGUID(&DXVA_COPPQueryLocalProtectionLevel,
                        &pStatusInput->guidStatusRequestID)) {
            Level = pThis->m_LocalLevel[ProtIndex];
        }
        else {
            Level = g_nLevels[ProtIndex] - 1;
            for ( ; Level != 0; Level--) {
                if (g_COPPLevels[pThis->m_DevID].Levels[ProtIndex][Level]) {
                    break;
                }
            }
        }
        DXVA_COPPStatusData Tmp;
        Tmp.rApp = pStatusInput->rApp;
        Tmp.dwData = Level;
        Tmp.dwFlags = COPP_StatusNormal;
        pStatusOutput->cbSizeData = sizeof(Tmp);
        memcpy(pStatusOutput->COPPStatus, &Tmp, sizeof(Tmp));
    }
    pThis->m_StatusSeqNumber++;
    pStatusOutput->macKDI = COPP_CalculateMAC(&pThis->m_AesHelper,
                                    (BYTE*)&pStatusOutput->cbSizeData,
                         sizeof(DXVA_COPPStatusOutput) - sizeof(GUID),
                                     &pThis->m_KDI);
    return NO_ERROR;
}
```

**必要条件**

| 対象プラットフォーム | バージョン |
| -- | -- |
| Desktop | この関数は、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。 |
