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
ms.openlocfilehash: cf4aee45fb98a422dc8d226e2448818af560f3d8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375821"
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

ドライバーを実行する方法の詳細についてはインター レースを解除またはによって提供される情報を使用して、フレーム レートの変換操作、 *lpVideoDescription*パラメーターを参照してください[インターのビデオのコンテンツとフレーム レート変換](https://docs.microsoft.com/windows-hardware/drivers/display/video-content-for-deinterlace-and-frame-rate-conversion)します。

サンプル*DeinterlaceOpenStream*関数のマップに直接、 **CreateMoComp**のメンバー、 [ **DD\_MOTIONCOMPCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)構造、GUID はインター モードを要求します。 **LpData**のメンバー、 [ **DD\_CREATEMOCOMPDATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_createmocompdata)へのポインターを構造体、 [ **DXVA\_VideoDesc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videodesc)構造体。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**DD\_MOTIONCOMPCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**DD\_CREATEMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_createmocompdata)

[**DeinterlaceQueryAvailableModes**](dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes.md)

[**DXVA\_VideoDesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videodesc)

 

 






