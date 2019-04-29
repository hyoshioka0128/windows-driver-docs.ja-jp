---
title: COPPOpenVideoSession 関数
description: COPPOpenVideoSession 関数のサンプルでは、現在のビデオ セッションに使用される COPP DirectX VA デバイス オブジェクトを初期化します。
ms.assetid: 4fc318c8-c999-4623-91da-3a3fea83d7b4
keywords:
- 保護 WDK COPP、ビデオのミニポート ドライバー コード テンプレートのコピーします。
- ビデオのコピー防止 WDK COPP、ビデオのミニポート ドライバー コード テンプレート
- 保護されたビデオ WDK COPP、ビデオのミニポート ドライバー コード テンプレート
- ビデオのミニポート ドライバー WDK Windows 2000、COPP コード テンプレート
- 認定済みの出力保護のプロトコル
ms.date: 02/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: ebf12e148b6df3cfbd273036dc0c308a41e35237
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331304"
---
# <a name="coppopenvideosession-function"></a>COPPOpenVideoSession 関数

COPPOpenVideoSession 関数のサンプルでは、現在のビデオ セッションに使用される COPP DirectX VA デバイス オブジェクトを初期化します。

### <a name="syntax"></a>構文

```cpp
HRESULT COPPOpenVideoSession(
  _In_ COPP_DeviceData pThis,
  _In_ ULONG           DevID
);
```

## <a name="parameters"></a>パラメーター

*[in] pThis*

* COPP DirectX VA デバイス オブジェクトへのポインター。

*[In] です。*

* COPP デバイスが接続されているグラフィックス デバイスの識別子を提供します。

## <a name="return-value"></a>戻り値

0 (S_OK または DD_OK) を返します成功した場合。それ以外の場合、エラー コードを返します。

## <a name="remarks"></a>注釈

COPP デバイス クラスの他のメンバー関数が呼び出される前に、COPPOpenVideoSession 呼び出しを通じて COPP デバイスを初期化する必要があります。 COPPOpenVideoSession は、それぞれのサポートされている保護の種類と対応するグローバルな保護レベルのカウンターをインクリメントのビデオ セッションのローカルでの保護レベル (0 に設定) を初期化する必要があります。 詳細については、保護レベルの処理を参照してください。

デュアル ビュー以外のモードを使用する複数のグラフィックス アダプター DevID パラメーターのドライブで識別されるデバイスの場合、COPPOpenVideoSession は DDERR_UNSUPPORTEDMODE を返す必要があります。 詳細については、COPP とマルチ モニター サポートを参照してください。

COPPOpenVideoSession 関数のサンプルは、DD_MOTIONCOMPCALLBACKS 構造体の CreateMoComp メンバーに直接マップされます。 CreateMoComp メンバーは、ディスプレイ ドライバーによって提供される DdMoCompCreate コールバックを参照する関数 DD_CREATEMOCOMPDATA 構造体を指します。 DD_CREATEMOCOMPDATA の lpGuid メンバーは、GUID COPP DirectX VA デバイスを指します。

## <a name="example-code"></a>コード例

次のコードでは、COPPOpenVideoSession 関数を実装する方法の例を示します。

```cpp
HRESULT
COPPOpenVideoSession(
    COPP_DeviceData* pThis,
    DWORD DevID
    )
{
    DWORD i;
    pThis->m_DevID = DevID;
    pThis->m_CmdSeqNumber = (DWORD)-1;
    pThis->m_StatusSeqNumber = (DWORD)-1;
    pThis->m_COPPDevState = COPP_OPENED;
    memset(&pThis->m_AesHelper, 0, sizeof(pThis->m_AesHelper));
    //
    // make sure the session protection levels are reset
    //
    memset(&pThis->m_LocalLevel, 0, sizeof(pThis->m_LocalLevel));
    //
    // initialize the session local protection levels and
    // increment the corresponding global protection level counter
    //
    // enumerate all the protection types supported by this connector
    DWORD j;
    for (j = COPP_ProtectionType_HDCP, i = COPP_ProtectionTypeIndex_HDCP;
         j & COPP_ProtectionType_Mask; j <<= 1, i++) {
        // for each type supported, make sure the initial level
        // is set correctly
        if (g_ConnectorInfo[pThis->m_DevID].ProtectionTypeMask & j) {
            pThis->m_LocalLevel[i] = 0;
            g_COPPLevels[pThis->m_DevID].Levels[i][0]++;
        }
        else {
            pThis->m_LocalLevel[i] = COPP_NoProtectionLevelAvailable;
        }
    }
    return NO_ERROR;
}
```

**必要条件**

| 対象プラットフォーム | バージョン |
| -- | -- |
| Desktop | この関数は、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。 |
