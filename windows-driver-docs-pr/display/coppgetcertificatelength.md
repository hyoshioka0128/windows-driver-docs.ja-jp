---
title: COPPGetCertificateLength 関数
description: COPPGetCertificateLength 関数のサンプルでは、グラフィックス ハードウェアで使用される証明書のバイト単位のサイズを取得します。
ms.assetid: 4a043c47-a5d2-4a7e-911c-9f57f7aa82cf
keywords:
- 保護 WDK COPP、ビデオのミニポート ドライバー コード テンプレートのコピーします。
- ビデオのコピー防止 WDK COPP、ビデオのミニポート ドライバー コード テンプレート
- 保護されたビデオ WDK COPP、ビデオのミニポート ドライバー コード テンプレート
- ビデオのミニポート ドライバー WDK Windows 2000、COPP コード テンプレート
ms.date: 02/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7d162c85630794490ae4596b2a4cab151370e002
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56531348"
---
# <a name="coppgetcertificatelength-function"></a>COPPGetCertificateLength 関数

COPPGetCertificateLength 関数のサンプルでは、グラフィックス ハードウェアで使用される証明書のバイト単位のサイズを取得します。

### <a name="syntax"></a>構文

```cpp
HRESULT COPPGetCertificateLength(
  _In_  COPP_DeviceData pThis,
  _Out_ ULONG           *pCertificateLength
);
```

## <a name="parameters"></a>パラメーター

*[in] pThis*

* COPP DirectX VA デバイス オブジェクトへのポインター。

*pCertificateLength [out]*

* グラフィックス ハードウェアで使用される証明書のバイト単位のサイズを受け取る変数へのポインター。

## <a name="return-value"></a>戻り値

0 (S_OK または DD_OK) を返します成功した場合。それ以外の場合、エラー コードを返します。

## <a name="remarks"></a>注釈

COPP DirectX VA デバイスは、その COPPGetCertificateLength 関数の呼び出しを受信する前に初期化する必要があります。 つまり、COPPGetCertificateLength する前に、COPPOpenVideoSession 関数を呼び出す必要があります。 COPPGetCertificateLength は COPPOpenVideoSession する前に呼び出されると、COPPGetCertificateLength は E_UNEXPECTED を返します。

## <a name="mapping-rendermocomp-to-coppgetcertificatelength"></a>COPPGetCertificateLength へ RenderMoComp のマッピング

COPPGetCertificateLength 関数のサンプルは、DD_MOTIONCOMPCALLBACKS 構造体の RenderMoComp メンバーへの呼び出しに直接マップされます。 RenderMoComp メンバーは、ディスプレイ ドライバーによって提供される DdMoCompRender コールバックを参照する関数 DD_RENDERMOCOMPDATA 構造体を指します。

RenderMoComp のコールバック関数が関数を使用せず、ディスプレイ ドライバーによって提供される BeginMoCompFrame または EndMoCompFrame 最初に呼び出されると呼ばれます。

DD_RENDERMOCOMPDATA 構造は次のように入力されます。

| メンバー | Value |
| -- | -- |
| dwNumBuffers | 0 を返します。 |
| lpBufferInfo | NULL:  |
| dwFunction | DXVA_COPPGetCertificateLengthFnCode 定数が (dxva.h で定義されている)。 |
| lpInputData | NULL:  |
| lpOutputData | ULONG 型指定された変数へのポインター。 |

## <a name="example-code"></a>コードの例

次のコードでは、COPPGetCertificateLength 関数を実装する方法の例を示します。

```cpp
HRESULT
COPPGetCertificateLength(
    COPP_DeviceData* pThis,
    DWORD* pCertificateLength
    )
{
    if (pThis->m_COPPDevState != COPP_OPENED) {
        return E_UNEXPECTED;
    }
    *pCertificateLength = sizeof(TestCert);
    pThis->m_COPPDevState = COPP_CERT_LENGTH_RETURNED;
    return NO_ERROR;
}
```

**要件**

| 対象プラットフォーム | バージョン |
| -- | -- |
| Desktop | この関数は、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。 |



