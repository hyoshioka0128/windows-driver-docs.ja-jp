---
title: DeinterlaceOpenStream メソッド
description: DXVA_DeinterlaceBobDeviceClass::DeinterlaceOpenStream 関数のサンプルでは、作成し、インター ストリーム オブジェクトを開きます。
ms.assetid: 975d5f6a-8d92-4da5-846c-1637fca58eb1
keywords:
- ディスプレイ デバイスの DeinterlaceOpenStream メソッド
- DeinterlaceOpenStream メソッド ディスプレイ デバイス、DXVA_DeinterlaceBobDeviceClass インターフェイス
- DXVA_DeinterlaceBobDeviceClass は、DeinterlaceOpenStream メソッドのディスプレイ デバイスをインターフェイスします。
topic_type:
- apiref
api_name:
- DXVA_DeinterlaceBobDeviceClass.DeinterlaceOpenStream
api_type:
- COM
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 614d6dfa6fdee4d9496af412031ef003828d8a20
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357684"
---
# <a name="dxvadeinterlacebobdeviceclassdeinterlaceopenstream-method"></a>DXVA\_DeinterlaceBobDeviceClass::DeinterlaceOpenStream メソッド


サンプル*DeinterlaceOpenStream*関数を作成し、インター ストリーム オブジェクトを開きます。

<a name="syntax"></a>構文
------

```cpp
HRESULT DeinterlaceOpenStream(
  [in] LPDXVA_VideoDesc lpVideoDescription
);
```

<a name="parameters"></a>パラメーター
----------

*lpVideoDescription* \[で\]へのポインターを提供する**DXVA\_VideoDesc**ハードウェア。

<a name="return-value"></a>戻り値
------------

0 を返します (S\_[ok] または DD\_OK) 成功した場合、それ以外の場合、エラー コードを返します。 参照してください*ddraw.h*エラー コードの完全な一覧についてはします。

<a name="remarks"></a>注釈
-------

使用して GUID を確認した後のインター モード、 [ **DeinterlaceQueryAvailableModes** ](dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes.md)関数、インター ストリーム オブジェクトを作成できます。 このオブジェクトは、任意のハードウェアを予約するディスプレイ ドライバーを使用できます。 要求されたを実行するために必要なリソース操作インター レースを解除します。

ドライバーを実行する方法の詳細についてはインター レースを解除またはによって提供される情報を使用して、フレーム レートの変換操作、 *lpVideoDescription*パラメーターを参照してください[インターのビデオのコンテンツとフレーム レート変換](https://msdn.microsoft.com/library/windows/hardware/ff570502)します。

サンプル*DeinterlaceOpenStream*関数のマップに直接、 **CreateMoComp**のメンバー、 [ **DD\_MOTIONCOMPCALLBACKS** ](https://msdn.microsoft.com/library/windows/hardware/ff551660)構造、GUID はインター モードを要求します。 **LpData**のメンバー、 [ **DD\_CREATEMOCOMPDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff550529)へのポインターを構造体、 [ **DXVA\_VideoDesc** ](https://msdn.microsoft.com/library/windows/hardware/ff564070)構造体。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**DD\_MOTIONCOMPCALLBACKS**](https://msdn.microsoft.com/library/windows/hardware/ff551660)

[**DD\_CREATEMOCOMPDATA**](https://msdn.microsoft.com/library/windows/hardware/ff550529)

[**DeinterlaceQueryAvailableModes**](dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes.md)

[**DXVA\_VideoDesc**](https://msdn.microsoft.com/library/windows/hardware/ff564070)

 

 






