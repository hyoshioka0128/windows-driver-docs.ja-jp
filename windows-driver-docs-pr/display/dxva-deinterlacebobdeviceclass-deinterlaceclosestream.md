---
title: DeinterlaceCloseStream メソッド
description: サンプルの DXVA\_DeinterlaceBobDeviceClass::DeinterlaceCloseStream 関数インター ストリーム オブジェクトを閉じるし、ストリームに関連付けられているすべてのハードウェア リソースを解放するデバイス ドライバーに指示します。
ms.assetid: 89131951-7d79-4236-9d9f-51382d63baa9
keywords:
- ディスプレイ デバイスの DeinterlaceCloseStream メソッド
- DeinterlaceCloseStream メソッド ディスプレイ デバイス、DXVA_DeinterlaceBobDeviceClass インターフェイス
- DXVA_DeinterlaceBobDeviceClass は、DeinterlaceCloseStream メソッドのディスプレイ デバイスをインターフェイスします。
topic_type:
- apiref
api_name:
- DXVA_DeinterlaceBobDeviceClass.DeinterlaceCloseStream
api_type:
- COM
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 752c7730ee7e47ca39e2e316bdaa1a99ee96498a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360360"
---
# <a name="dxvadeinterlacebobdeviceclassdeinterlaceclosestream-method"></a>DXVA\_DeinterlaceBobDeviceClass::DeinterlaceCloseStream メソッド


サンプル*DeinterlaceCloseStream*関数インター ストリーム オブジェクトを閉じるし、ストリームに関連付けられているすべてのハードウェア リソースを解放するデバイス ドライバーに指示します。

<a name="syntax"></a>構文
------

```cpp
HRESULT DeinterlaceCloseStream();
```

<a name="parameters"></a>パラメーター
----------

このメソッドにはパラメーターはありません。

<a name="return-value"></a>戻り値
------------

0 を返します (S\_[ok] または DD\_OK) 成功した場合、それ以外の場合、エラー コードを返します。 参照してください*ddraw.h*エラー コードの完全な一覧についてはします。

<a name="remarks"></a>注釈
-------

*DeinterlaceCloseStream*関数のマップに直接、 **DestroyMoComp**のメンバー、 [ **DD\_MOTIONCOMPCALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551660)ドライバーによって提供されるを指す構造体*DdMoCompDestroy*コールバック。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**DD\_MOTIONCOMPCALLBACKS**](https://msdn.microsoft.com/library/windows/hardware/ff551660)

[**DeinterlaceOpenStream**](dxva-deinterlacebobdeviceclass-deinterlaceopenstream.md)

 

 






