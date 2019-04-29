---
title: COPPCommand 関数
description: COPPCommand 関数のサンプルでは、COPP DirectX VA デバイスで操作を実行します。
ms.assetid: 917628be-e965-4ca4-bfa8-0e80476df153
keywords:
- 保護 WDK COPP、ビデオのミニポート ドライバー コード テンプレートのコピーします。
- ビデオのコピー防止 WDK COPP、ビデオのミニポート ドライバー コード テンプレート
- 保護されたビデオ WDK COPP、ビデオのミニポート ドライバー コード テンプレート
- ビデオのミニポート ドライバー WDK Windows 2000、COPP コード テンプレート
- 認定済みの出力保護のプロトコル
ms.date: 02/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: 32d0be8fe821eb2beec0a0cb9064c635cfa2459d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331310"
---
# <a name="coppcommand-function"></a>COPPCommand 関数

COPPCommand 関数のサンプルでは、COPP DirectX VA デバイスで操作を実行します。

## <a name="syntax"></a>構文

```cpp
HRESULT COPPCommand(
  _In_ COPP_DeviceData  pThis,
  _In_ DXVA_COPPCommand *pCommand
);
```

## <a name="parameters"></a>パラメーター

*[in] pThis*

 * COPP DirectX VA デバイス オブジェクトへのポインター。

*[in] pCommand*
* COPP デバイスで実行する操作に関する情報を含む DXVA_COPPCommand 構造体へのポインターを提供します。

## <a name="return-value"></a>戻り値

0 (S_OK または DD_OK) を返します成功した場合。それ以外の場合、エラー コードを返します。

## <a name="remarks"></a>注釈

ビデオのセッションは、保護モードに設定する必要があります (つまり、必要がある active) 関連付けられている COPP DirectX VA する前にデバイスがその COPPCommand 関数の呼び出しを受信します。 つまり、COPPCommand する前に、COPPSequenceStart 関数を呼び出す必要があります。 COPPCommand は COPPSequenceStart する前に呼び出されると、COPPCommand は E_UNEXPECTED を返します。

COPPCommand 関数は、COPP コマンドが含まれるデータが設定された DXVA_COPPCommand 構造体を受け取ります。 次の COPP コマンドがサポートされています。

* **DXVA_COPPSetProtectionLevel** <br>物理的なコネクタの保護レベルを設定するには、ビデオのセッションから命令は、COPP デバイスに関連付けられています。 ビデオのミニポート ドライバーは、同じ物理 connector を介してコンテンツを再生すべて複数のビデオ セッションをサポートできる必要があります。
* **DXVA_COPPSetSignaling** <br>DirectX VA COPP デバイスに関連付けられた物理コネクタを通過する信号を保護する方法についての命令です。

COPPCommand 関数は渡されたパラメーターが使用されている特定の物理コネクタは有効であることを確認する必要があり、E_INVALIDARG 場合は、1 つまたは複数のパラメーターに無効なを返す必要があります。

COPPCommand に渡される保護コマンドは、モニターのディスプレイの解像度と互換性がない、COPPCommand は DDERR_TOOBIGSIZE を返す必要があります。

## <a name="mapping-rendermocomp-to-coppcommand"></a>COPPCommand へ RenderMoComp のマッピング

COPPCommand 関数のサンプルは、DD_MOTIONCOMPCALLBACKS 構造体の RenderMoComp メンバーへの呼び出しに直接マップされます。 RenderMoComp メンバーは、ディスプレイ ドライバーによって提供される DdMoCompRender コールバックを参照する関数 DD_RENDERMOCOMPDATA 構造体を指します。

RenderMoComp のコールバック関数が関数を使用せず、ディスプレイ ドライバーによって提供される BeginMoCompFrame または EndMoCompFrame 最初に呼び出されると呼ばれます。

DD_RENDERMOCOMPDATA 構造は次のように入力されます。

| Member | 値 |
| -- | -- |
| dwNumBuffers | 0 を返します。 |
| lpBufferInfo | NULL:  |
| dwFunction | DXVA_COPPCommandFnCode 定数が (dxva.h で定義されている)。|
| lpInputData | DXVA_COPPCommand 構造体へのポインター。 |
| lpOutputData | NULL:  |

## <a name="example-code"></a>コードの例

次のコードでは、COPPCommand 関数を実装する方法の例を示します。

```cpp
GUID
COPP_CalculateMAC(
    AESHelper* pAesHelper,
    BYTE* pInputData,
    DWORD dwDataLength,
    GUID* pKDI
    )
{
    GUID rgbTag;
    memset(&rgbTag, 0, sizeof(GUID));
    SignData(pAesHelper, pInputData, dwDataLength, (BYTE*)&rgbTag);
    return rgbTag;
}

HRESULT
COPPCommand(
    COPP_DeviceData* pThis,
    DXVA_COPPCommand* pCommand
    )
{
    DXVA_COPPSetProtectionLevelCmdData CmdData;
    DWORD ProtIndex = COPP_ProtectionTypeIndex_Unkonwn;
    if (pThis->m_COPPDevState != COPP_SESSION_ACTIVE) {
        return E_UNEXPECTED;
    }
    if (pCommand->dwSequence != pThis->m_CmdSeqNumber) {
        return E_INVALIDARG;
    }
    if (!IsEqualGUID(&pCommand->guidCommandID, &DXVA_COPPSetProtectionLevel)) {
        return E_INVALIDARG;
    }
    //
    // ensure that enough data is passed
    //
    if (pCommand->cbSizeData < sizeof(DXVA_COPPSetProtectionLevelCmdData)) {
        return E_INVALIDARG;
    }
    //
    // verify that the command message was sent by the application
    // over the secure channel by validating the MAC on the message
    //
    GUID macCalculated = COPP_CalculateMAC(&pThis->m_AesHelper,
                                      (BYTE*)&pCommand->guidCommandID,
                              sizeof(DXVA_COPPCommand) - sizeof(GUID),
                                       &pThis->m_KDI);
        if (!IsEqualGUID(&macCalculated, &pCommand->macKDI)) {
            return E_UNEXPECTED;
        }
    memcpy(&CmdData, pCommand->CommandData, sizeof(DXVA_COPPSetProtectionLevelCmdData));
    //
    // determine which protection level (CmdData.ProtType) was passed and
    // set ProtIndex accordingly (for example, ProtIndex = COPP_ProtectionTypeIndex_ACP)
    //
    //
    // ensure that the request is valid
    //
    if (CmdData.ProtLevel >= g_nLevels[ProtIndex]) {
        return E_INVALIDARG;
    }
    // set the new local level and store the former local level
    DWORD oldLevel = pThis->m_LocalLevel[ProtIndex];
    pThis->m_LocalLevel[ProtIndex] = CmdData.ProtLevel;
    // decrement the former global level and increment the new
    g_COPPLevels[pThis->m_DevID].Levels[ProtIndex][oldLevel]--;
    g_COPPLevels[pThis->m_DevID].Levels[ProtIndex][CmdData.ProtLevel]++;
    pThis->m_CmdSeqNumber++;
    return NO_ERROR;
}
```

**必要条件**

|対象プラットフォーム | バージョン |
| -- | -- |
| Desktop | この関数は、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。 |



