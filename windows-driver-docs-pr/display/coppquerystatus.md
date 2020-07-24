---
title: COPPQueryStatus 関数
description: Sample COPPQueryStatus 関数は、COPP DirectX VA デバイスに関連付けられている、保護されたビデオセッションの状態を取得します。
ms.assetid: c2265df7-8b60-4a14-b7dc-ee227ad062dc
keywords:
- コピー防止 WDK COPP、ビデオミニポートドライバーコードテンプレート
- ビデオコピー防止 WDK COPP、ビデオミニポートドライバーコードテンプレート
- protected video WDK COPP、ビデオミニポートドライバーコードテンプレート
- ビデオミニポートドライバー WDK Windows 2000、COPP コードテンプレート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef7ba2580ec60903c9398d4112493bb60ea3d6e1
ms.sourcegitcommit: df50dc10210c124f2c7fb173d6e4fb796f56e5bd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/22/2020
ms.locfileid: "86949724"
---
# <a name="coppquerystatus-function"></a>COPPQueryStatus 関数

Sample COPPQueryStatus 関数は、COPP DirectX VA デバイスに関連付けられている、保護されたビデオセッションの状態を取得します。

### <a name="syntax"></a>構文

```cpp
HRESULT COPPQueryStatus(
  _In_  COPP_DeviceData       pThis,
  _In_  DXVA_COPPStatusInput  *pInput,
  _Out_ DXVA_COPPStatusOutput *pOutput
);
```

## <a name="parameters"></a>パラメーター

*pThis [in]*

* COPP DirectX VA デバイスオブジェクトへのポインター。

*pInput [入力]*

* 特定のステータス情報を取得する要求を含む DXVA_COPPStatusInput 構造体へのポインターを提供します。

*pOutput [出力]*

* 使用されている物理コネクタに関するステータス情報を受け取る DXVA_COPPStatusOutput 構造体へのポインター。

## <a name="return-value"></a>戻り値

成功した場合は 0 (S_OK または DD_OK) を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>注釈

関連する COPP DirectX VA デバイスが COPPQueryStatus 関数への呼び出しを受け取る前に、ビデオセッションを保護モードに設定する必要があります (つまり、アクティブにする必要があります)。 つまり、COPPQueryStatus の前に、COPPSequenceStart 関数を呼び出す必要があります。 COPPQueryStatus が COPPSequenceStart の前に呼び出された場合、COPPQueryStatus は E_UNEXPECTED を返す必要があります。

COPPQueryStatus 関数は、ステータス要求を含む pInput で設定された DXVA_COPPStatusInput 構造体を受け取ります。 COPPQueryStatus 関数は、要求を処理し、pOutput の DXVA_COPPStatusOutput 構造体に適切な状態を返します。

## <a name="mapping-rendermocomp-to-coppquerystatus"></a>RenderMoComp から COPPQueryStatus へのマッピング

Sample COPPQueryStatus 関数は、DD_MOTIONCOMPCALLBACKS 構造体の RenderMoComp メンバーへの呼び出しに直接マップされます。 RenderMoComp メンバーは、DD_RENDERMOCOMPDATA 構造体を参照するディスプレイドライバーが提供する DdMoCompRender コールバック関数を指します。

RenderMoComp コールバック関数が呼び出されるのは、表示ドライバーが提供する BeginMoCompFrame または EndMoCompFrame 関数が最初に呼び出されない場合です。

DD_RENDERMOCOMPDATA 構造体は次のように入力されます。

| メンバー | 値 |
| ------ | ----- |
| dwNumBuffers | ゼロ。 |
| lpBufferInfo | NULL。 |
| dwFunction | DXVA_COPPQueryStatusFnCode 定数 (DXVA で定義)。 |
| lpInputData | DXVA_COPPStatusInput 構造体へのポインター。 |
| lpOutputData | DXVA_COPPStatusOutput 構造体へのポインター。 |

## <a name="example-code"></a>コード例

次のコードは、COPPQueryStatus 関数を実装する方法の例を示しています。

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

| ターゲット プラットフォーム | Version |
| -- | -- |
| デスクトップ | この機能は、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。 |
