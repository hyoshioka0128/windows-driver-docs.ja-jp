---
title: DeinterlaceOpenStream メソッド
description: Sample DXVA_DeinterlaceBobDeviceClass::D einterlaceOpenStream 関数は、ノンインターレースストリームオブジェクトを作成して開きます。
ms.assetid: 975d5f6a-8d92-4da5-846c-1637fca58eb1
keywords:
- DeinterlaceOpenStream メソッドの表示デバイス
- DeinterlaceOpenStream メソッドの表示デバイス, DXVA_DeinterlaceBobDeviceClass インターフェイス
- DXVA_DeinterlaceBobDeviceClass インターフェイス表示デバイス, DeinterlaceOpenStream メソッド
topic_type:
- apiref
api_name:
- DXVA_DeinterlaceBobDeviceClass.DeinterlaceOpenStream
api_type:
- COM
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: d5b2a01fc74d0c2bc76638d01d40b70ef2ed3709
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838967"
---
# <a name="dxva_deinterlacebobdeviceclassdeinterlaceopenstream-method"></a>DXVA\_DeinterlaceBobDeviceClass::D einterlaceOpenStream メソッド


Sample *DeinterlaceOpenStream*関数は、ノンインターレースストリームオブジェクトを作成して開きます。

<a name="syntax"></a>構文
------

```cpp
HRESULT DeinterlaceOpenStream(
  [in] LPDXVA_VideoDesc lpVideoDescription
);
```

<a name="parameters"></a>パラメーター
----------

\] の*Lpvideodescription* \[は、 **DXVA\_videodesc**ハードウェアへのポインターを提供します。

<a name="return-value"></a>戻り値
------------

成功した場合は 0 (S\_OK または DD\_OK) を返します。それ以外の場合は、エラーコードを返します。 エラーコードの完全な一覧については、 *ddraw*を参照してください。

<a name="remarks"></a>注釈
-------

[**DeinterlaceQueryAvailableModes**](dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes.md)関数を使用してノンインターレースモード GUID が見つかった後、ノンインターレースストリームオブジェクトを作成できます。 このオブジェクトを使用すると、表示ドライバーは、要求されたインターレース解除操作を実行するために必要なハードウェアリソースを予約できます。

*Lpvideodescription*パラメーターによって指定された情報を使用してドライバーがインターレース解除操作またはフレームレート変換操作を実行する方法の詳細については、「[インターレース解除とフレームレート変換のビデオコンテンツ](https://docs.microsoft.com/windows-hardware/drivers/display/video-content-for-deinterlace-and-frame-rate-conversion)」を参照してください。

Sample *DeinterlaceOpenStream*関数は、 [**DD\_MOTIONCOMPCALLBACKS バック**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)構造の**createmocomp**メンバーに直接マップします。 GUID は、要求されたノンインターレースモードです。 [**DD\_CREATEMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_createmocompdata)構造体の**lpData**メンバーは、 [**DXVA\_videodesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)構造体を指します。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**DD\_MOTIONCOMPCALLBACKS バック**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**DD\_CREATEMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_createmocompdata)

[**DeinterlaceQueryAvailableModes**](dxva-deinterlacecontainerdeviceclass-deinterlacequeryavailablemodes.md)

[**DXVA\_VideoDesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)

 

 






