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
ms.openlocfilehash: bc53cabb284afc2d92a41e74e5d3b9f4a7cb7a78
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579212"
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

* * [なし]

<a name="return-value"></a>戻り値
------------

0 を返します (S\_[ok] または DD\_OK) 成功した場合、それ以外の場合、エラー コードを返します。 参照してください*ddraw.h*エラー コードの完全な一覧についてはします。

<a name="remarks"></a>コメント
-------

**ProcAmpControlCloseStream**関数のマップに直接、 **DestroyMoComp**のメンバー、 [ **DD\_MOTIONCOMPCALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551660)構造体は、ドライバーによって提供される指す[ *DdMoCompDestroy* ](https://msdn.microsoft.com/library/windows/hardware/ff549664)コールバック。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**DD\_MOTIONCOMPCALLBACKS**](https://msdn.microsoft.com/library/windows/hardware/ff551660)

[**ProcAmpControlOpenStream**](dxva-procampcontroldeviceclass-procampcontrolopenstream.md)

 

 






