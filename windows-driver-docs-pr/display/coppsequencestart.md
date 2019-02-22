---
title: COPPSequenceStart 関数
description: COPPSequenceStart 関数のサンプルでは、現在のビデオ セッションを保護モードに設定します。
ms.assetid: c3b3d4ad-ab86-4cc4-9023-8b0cd0655d42
keywords:
- 保護 WDK COPP、ビデオのミニポート ドライバー コード テンプレートのコピーします。
- ビデオのコピー防止 WDK COPP、ビデオのミニポート ドライバー コード テンプレート
- 保護されたビデオ WDK COPP、ビデオのミニポート ドライバー コード テンプレート
- ビデオのミニポート ドライバー WDK Windows 2000、COPP コード テンプレート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fa73c53c7b472bb2fe49b138e33de8c749a4af6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537062"
---
# <a name="coppsequencestart-function"></a>COPPSequenceStart 関数

COPPSequenceStart 関数のサンプルでは、現在のビデオ セッションを保護モードに設定します。

### <a name="syntax"></a>構文

```cpp
HRESULT COPPSequenceStart(
  _In_ COPP_DeviceData    pThis,
  _In_ DXVA_COPPSignature *pSeqStartInfo
);
```

## <a name="parameters"></a>パラメーター

*[in] pThis*

* COPP DirectX VA デバイス オブジェクトへのポインター。

*pSeqStartInfo [in]*

* シーケンスの開始に関する情報を格納する DXVA_COPPSignature 構造体へのポインターを提供します。

## <a name="return-value"></a>戻り値

0 (S_OK または DD_OK) を返します成功した場合。それ以外の場合、エラー コードを返します。

## <a name="remarks"></a>注釈

COPP DirectX VA デバイスは、その COPPSequenceStart 関数の呼び出しを受信する前に、VMR にグラフィックス ハードウェアの証明書を提供する必要があります。 つまり、COPPSequenceStart する前に、COPPKeyExchange 関数を呼び出す必要があります。 COPPSequenceStart は COPPKeyExchange する前に呼び出されると、COPPSequenceStart は E_UNEXPECTED を返します。

グラフィックス ハードウェアの証明書を提供するには後、COPP DirectX VA デバイスはその COPPSequenceStart 関数への 1 つだけの呼び出しを受信する必要があります。 COPP DirectX VA デバイスは、別の COPPSequenceStart 呼び出しを受信する場合は E_UNEXPECTED を返します。

COPPSequenceStart 関数は、次のものを連結して 1 つから成る開始シーケンスを含むデータが設定された DXVA_COPPSignature 構造体を受け取ります。

* ドライバーによって生成され、ドライバーの COPPKeyExchange 関数の呼び出しによって返される 128 ビットのランダムな数値
* 128 ビットのランダムなデータ整合性のセッション キー
* ランダムな開始状態のシーケンス番号の 32 ビット
* ランダムな開始コマンドのシーケンス番号の 32 ビット

開始シーケンスは、グラフィック ハードウェアの公開キーを使用して暗号化されます。

## <a name="mapping-rendermocomp-to-coppsequencestart"></a>COPPSequenceStart へ RenderMoComp のマッピング

COPPSequenceStart 関数のサンプルは、DD_MOTIONCOMPCALLBACKS 構造体の RenderMoComp メンバーへの呼び出しに直接マップされます。 RenderMoComp メンバーは、ディスプレイ ドライバーによって提供される DdMoCompRender コールバックを参照する関数 DD_RENDERMOCOMPDATA 構造体を指します。

RenderMoComp のコールバック関数が関数を使用せず、ディスプレイ ドライバーによって提供される BeginMoCompFrame または EndMoCompFrame 最初に呼び出されると呼ばれます。

DD_RENDERMOCOMPDATA 構造は次のように入力されます。

| メンバー | Value |
| -- | -- |
| dwNumBuffers | 0 を返します。 |
| lpBufferInfo | NULL:  |
| dwFunction | DXVA_COPPSequenceStartFnCode 定数が (dxva.h で定義されている)。 |
| lpInputData | DXVA_COPPSignature 構造体へのポインター。 |
| lpOutputData | NULL:  |

## <a name="example-code"></a>コードの例

次のコードでは、COPPSequenceStart 関数を実装する方法の例を示します。

```cpp
HRESULT
COPP_RSADecryptData(
    const BYTE* lpPrivateKey,
    DXVA_COPPSignature* pOutput,
    DXVA_COPPSignature* pInput
    )
{
    DWORD dwLen = sizeof(DXVA_COPPSignature);
    return RSADecPrivate(lpPrivateKey, (const BYTE *)pInput,
                         sizeof(DXVA_COPPSignature), (BYTE*) pOutput, &dwLen);
}

HRESULT
COPPSequenceStart(
    COPP_DeviceData* pThis,
    DXVA_COPPSignature* pSeqStartInfo
    )
{
    if (pThis->m_COPPDevState == COPP_KEY_EXCHANGED) {
        BYTE* pByte;
        DXVA_COPPSignature Decrypted;
        GUID rGraphicsDriver;
        HRESULT hr;
        COPP_RSADecryptData(PrivateKey, &Decrypted, pSeqStartInfo);
        pByte = (BYTE*)&Decrypted;
        memcpy(&rGraphicsDriver, pByte, sizeof(DWORD));
        pByte += sizeof(DWORD);
        memcpy(&pThis->m_KDI, pByte, sizeof(GUID));
        pByte += sizeof(GUID);
        memcpy(&pThis->m_StatusSeqNumber, pByte, sizeof(DWORD));
        pByte += sizeof(DWORD);
        memcpy(&pThis->m_CmdSeqNumber, pByte, sizeof(DWORD));
        pByte += sizeof(DWORD);
        hr = SetKey(&pThis->m_AesHelper, (BYTE*)&pThis->m_KDI, sizeof(GUID));
        if (hr != S_OK) {
            return hr;
        }
        if (!IsEqualGUID(&rGraphicsDriver, &pThis->m_rGraphicsDriver)) {
            return E_UNEXPECTED;
        }
        pThis->m_COPPDevState = COPP_SESSION_ACTIVE;
    }
    else {
        return E_UNEXPECTED;
    }
    return NO_ERROR;
}
```

**要件**

| 対象プラットフォーム | バージョン |
| -- | -- |
| Desktop | この関数は、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。 |

