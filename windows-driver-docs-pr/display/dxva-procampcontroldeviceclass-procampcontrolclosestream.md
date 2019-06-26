---
title: ProcAmpControlCloseStream メソッド
description: サンプルの DXVA\_ProcAmpControlDeviceClass::ProcAmpCloseStream 関数 ProcAmp ストリーム オブジェクトを閉じるし、ストリームに関連付けられたハードウェア リソースを解放するデバイス ドライバーに指示します。
ms.assetid: aa13efb8-2014-4790-b121-cd9fd3171458
keywords:
- ディスプレイ デバイスの ProcAmpControlCloseStream メソッド
- ProcAmpControlCloseStream メソッド ディスプレイ デバイス、DXVA_ProcAmpControlDeviceClass インターフェイス
- DXVA_ProcAmpControlDeviceClass は、ProcAmpControlCloseStream メソッドのディスプレイ デバイスをインターフェイスします。
topic_type:
- apiref
api_name:
- DXVA_ProcAmpControlDeviceClass.ProcAmpControlCloseStream
api_type:
- COM
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 1aa6b4d6ff0207581b2a11bc1e43c1c75c4c28b3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383099"
---
# <a name="dxvaprocampcontroldeviceclassprocampcontrolclosestream-method"></a>DXVA\_ProcAmpControlDeviceClass::ProcAmpControlCloseStream メソッド


サンプル**ProcAmpCloseStream**関数 ProcAmp ストリーム オブジェクトを閉じるし、ストリームに関連付けられたハードウェア リソースを解放するデバイス ドライバーに指示します。

<a name="syntax"></a>構文
------

```cpp
HRESULT ProcAmpControlCloseStream(
   void
);
```

<a name="parameters"></a>パラメーター
----------

\* * [なし]

<a name="return-value"></a>戻り値
------------

0 を返します (S\_[ok] または DD\_OK) 成功した場合、それ以外の場合、エラー コードを返します。 参照してください*ddraw.h*エラー コードの完全な一覧についてはします。

<a name="remarks"></a>注釈
-------

**ProcAmpControlCloseStream**関数のマップに直接、 **DestroyMoComp**のメンバー、 [ **DD\_MOTIONCOMPCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)構造体は、ドライバーによって提供される指す[ *DdMoCompDestroy* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_destroy)コールバック。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**DD\_MOTIONCOMPCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**ProcAmpControlOpenStream**](dxva-procampcontroldeviceclass-procampcontrolopenstream.md)

 

 






