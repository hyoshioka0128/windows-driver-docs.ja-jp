---
title: COPPKeyExchange 関数
description: COPPKeyExchange 関数のサンプルでは、グラフィックス ハードウェアで使用されるデジタル証明書を取得します。
ms.assetid: ecf26fc7-fba0-4dcf-9b63-9808b8efec13
keywords:
- 保護 WDK COPP、ビデオのミニポート ドライバー コード テンプレートのコピーします。
- ビデオのコピー防止 WDK COPP、ビデオのミニポート ドライバー コード テンプレート
- 保護されたビデオ WDK COPP、ビデオのミニポート ドライバー コード テンプレート
- ビデオのミニポート ドライバー WDK Windows 2000、COPP コード テンプレート
ms.date: 02/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: 14d2690e1f9387e02b327202a3d3a8df239a78ab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331302"
---
# <a name="coppkeyexchange-function"></a>COPPKeyExchange 関数

COPPKeyExchange 関数のサンプルでは、グラフィックス ハードウェアで使用されるデジタル証明書を取得します。

### <a name="syntax"></a>構文

```cpp
HRESULT COPPKeyExchange(
  _In_  COPP_DeviceData pThis,
  _Out_ GUID            *pRandom,
  _Out_ BYTE            *pGHCertificate
);
```

## <a name="parameters"></a>パラメーター

*[in] pThis*

* COPP DirectX VA デバイス オブジェクトへのポインター。

*pRandom [out]*

* 128 ビットのランダムな数値を受け取る変数へのポインター。

*[out] pGHCertificate*

* グラフィックス ハードウェアの証明書を受信するバイトのリストへのポインター。

## <a name="return-value"></a>戻り値

0 (S_OK または DD_OK) を返します成功した場合。それ以外の場合、エラー コードを返します。

## <a name="remarks"></a>注釈

COPP DirectX VA デバイスは、その COPPKeyExchange 関数の呼び出しを受信する前に、VMR をグラフィックス ハードウェアの証明書のサイズを指定する必要があります。 つまり、COPPKeyExchange する前に、COPPGetCertificateLength 関数を呼び出す必要があります。 COPPKeyExchange は COPPGetCertificateLength する前に呼び出されると、COPPKeyExchange は E_UNEXPECTED を返します。

## <a name="mapping-rendermocomp-to-coppkeyexchange"></a>COPPKeyExchange へ RenderMoComp のマッピング

COPPKeyExchange 関数のサンプルは、DD_MOTIONCOMPCALLBACKS 構造体の RenderMoComp メンバーへの呼び出しに直接マップされます。 RenderMoComp メンバーは、ディスプレイ ドライバーによって提供される DdMoCompRender コールバックを参照する関数 DD_RENDERMOCOMPDATA 構造体を指します。

RenderMoComp のコールバック関数が関数を使用せず、ディスプレイ ドライバーによって提供される BeginMoCompFrame または EndMoCompFrame 最初に呼び出されると呼ばれます。

DD_RENDERMOCOMPDATA 構造は次のように入力されます。

| Member | 値 |
|--|--|
| dwNumBuffers | LpBufferInfo でバッファーの数。 値には 1 です。 |
| lpBufferInfo | ハードウェアの証明書を保持するために必要な領域を含む 1 つの RGB32 システム メモリ サーフェスへのポインター。 COPPGetCertificateLength への呼び出しに必要なサーフェスの長さが返されました。 <br>システム メモリのサーフェスを使用する証明書のサイズが lpOutputData パラメーターを通じて渡されるバッファーの最大値のサイズを超えているため、証明書を返すことに注意してください。|
| dwFunction | DXVA_COPPKeyExchangeFnCode 定数が (dxva.h で定義されている)。 |
| lpInputData | NULL:  |
| lpOutputData | ドライバーによって生成される 128 ビットのランダムな番号へのポインター。 |

## <a name="example-code"></a>コードの例

次のコードでは、COPPKeyExchange 関数を実装する方法の例を示します。

```cpp
DWORD
COPP_Generate128BitRandomNumber()
{
    GUID RandNum;
    DWORD* pdw = (DWORD*)&RandNum;
    pdw[0] = rand();
    pdw[1] = rand();
    pdw[2] = rand();
    pdw[3] = rand();
    return RandNum;
}

HRESULT
COPPKeyExchange(
    COPP_DeviceData* pThis,
    GUID* pRandNumber,
    BYTE* pGHCertificate
    )
{
    if (pThis->m_COPPDevState != COPP_CERT_LENGTH_RETURNED) {
        return E_UNEXPECTED;
    }
    memcpy(pGHCertificate, (LPVOID)&TestCert, sizeof(TestCert));
    pThis->m_rGraphicsDriver = *pRandNumber = COPP_Generate128BitRandomNumber();
    pThis->m_COPPDevState = COPP_KEY_EXCHANGED;
    return NO_ERROR;
}
```

**必要条件**

| 対象プラットフォーム | バージョン |
| -- | -- |
| Desktop |  この関数は、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。 |



