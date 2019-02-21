---
title: COPPCloseVideoSession 関数
description: COPPCloseVideoSession 関数のサンプルでは、現在のビデオ セッションに使用される COPP DirectX VA デバイス オブジェクトを閉じます。
ms.assetid: 27a6a23d-e9e8-403e-87b9-3ab0a07789cb
keywords:
- 保護 WDK COPP、ビデオのミニポート ドライバー コード テンプレートのコピーします。
- ビデオのコピー防止 WDK COPP、ビデオのミニポート ドライバー コード テンプレート
- 保護されたビデオ WDK COPP、ビデオのミニポート ドライバー コード テンプレート
- ビデオのミニポート ドライバー WDK Windows 2000、COPP コード テンプレート
- 認定済みの出力保護のプロトコル
ms.date: 02/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1b7f834af8092318730cc21061694c29241b3755
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56528060"
---
# <a name="coppclosevideosession-function"></a>COPPCloseVideoSession 関数

COPPCloseVideoSession 関数のサンプルでは、現在のビデオ セッションに使用される COPP DirectX VA デバイス オブジェクトを閉じます。

### <a name="syntax"></a>構文

```cpp
HRESULT COPPCloseVideoSession(
  _In_ COPP_DeviceData pThis
);
```

## <a name="parameters"></a>パラメーター

*[in] pThis*

* COPP DirectX VA デバイス オブジェクトへのポインター。

## <a name="return-value"></a>戻り値

0 (S_OK または DD_OK) を返します成功した場合。それ以外の場合、エラー コードを返します。

## <a name="remarks"></a>注釈

ビデオ セッションによって出力保護が適用されて引き続き COPPCloseVideoSession 関数を呼び出すことができます。 COPPCloseVideoSession の COPP DirectX VA デバイス オブジェクトの保護設定を元に戻すし、グローバルの保護設定を調整する必要がありますそれに応じて。

COPPCloseVideoSession 関数は、DD_MOTIONCOMPCALLBACKS 構造体の DestroyMoComp メンバーに直接マップされます。 DestroyMoComp メンバーは、ディスプレイ ドライバーによって提供される DdMoCompDestroy のコールバック関数を指します。

## <a name="example-code"></a>コード例

次のコードでは、COPPCloseVideoSession 関数を実装する方法の例を示します。

```cpp
HRESULT
COPPCloseVideoSession(
    COPP_DeviceData* pThis
    )
{
    DWORD j, i;
    // enumerate all the protection types supported by this connector
    for (j = COPP_ProtectionType_HDCP, i = COPP_ProtectionTypeIndex_HDCP;
         j & COPP_ProtectionType_Mask; j <<= 1, i++) {
        // for each type supported, make sure the initial level
        // is set correctly
        if (g_ConnectorInfo[pThis->m_DevID].ProtectionTypeMask & j) {
            DWORD oldLevel = pThis->m_LocalLevel[i];
            g_COPPLevels[pThis->m_DevID].Levels[i][oldLevel]--;
        }
    }
    ResetKey(&pThis->m_AesHelper);
    return NO_ERROR;
}
```

**要件**

| 対象プラットフォーム | バージョン |
| -- | -- |
| Desktop | この関数は、Windows Server 2003 SP1 以降、および Windows XP SP2 以降にのみ適用されます。 |
