---
title: ProcAmpControlOpenStream メソッド
description: Sample DXVA\_ProcAmpControlDeviceClass::P rocAmpControlOpenStream 関数は、ProcAmp stream オブジェクトを作成します。
ms.assetid: 73011ce3-f643-4fca-bcfd-1467a9b56181
keywords:
- ProcAmpControlOpenStream メソッドの表示デバイス
- ProcAmpControlOpenStream メソッドの表示デバイス, DXVA_ProcAmpControlDeviceClass インターフェイス
- DXVA_ProcAmpControlDeviceClass インターフェイス表示デバイス, ProcAmpControlOpenStream メソッド
topic_type:
- apiref
api_name:
- DXVA_ProcAmpControlDeviceClass.ProcAmpControlOpenStream
api_type:
- COM
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 35c43f685416ae21d51ed5535ff1d11bba5a5b60
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839711"
---
# <a name="dxva_procampcontroldeviceclassprocampcontrolopenstream-method"></a>DXVA\_ProcAmpControlDeviceClass::P rocAmpControlOpenStream メソッド


Sample *ProcAmpControlOpenStream*関数は、ProcAmp stream オブジェクトを作成します。

<a name="syntax"></a>構文
------

```cpp
HRESULT ProcAmpControlOpenStream(
  [in] LPDXVA_VideoDesc lpVideoDescription
);
```

<a name="parameters"></a>parameters
----------

\] の*Lpvideodescription* \[は、処理するビデオの ProcAmp コントロールパラメーターを定義する[**DXVA\_videodesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)構造体へのポインターを提供します。

<a name="return-value"></a>戻り値
------------

成功した場合は 0 (S\_OK または DD\_OK) を返します。それ以外の場合は、エラーコードを返します。 エラーコードの完全な一覧については、 *ddraw*を参照してください。

<a name="remarks"></a>解説
-------

*VMR*が[**ProcAmpControlQueryCaps**](dxva-deinterlacecontainerdeviceclass-procampcontrolquerycaps.md)および[**ProcAmpControlQueryRange**](dxva-deinterlacecontainerdeviceclass-procampcontrolqueryrange.md)関数を使用して ProcAmp control ハードウェアの機能と範囲を決定したら、ProcAmp stream オブジェクトを作成できます。 ProcAmp stream オブジェクトを作成すると、ディスプレイドライバーは、ProcAmp 調整操作を実行するために必要なハードウェアリソースを予約できます。

*ProcAmpControlOpenStream*関数は、 [**DD\_MOTIONCOMPCALLBACKS バック**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)構造の createmocomp メンバーへの呼び出しに直接マップされます。 CreateMoComp メンバーは、 [**DD\_CREATEMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_createmocompdata)構造体を参照するドライバーによって提供される関数を指します。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>関連項目


[**DXVA\_VideoDesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)

[**DD\_MOTIONCOMPCALLBACKS バック**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**DD\_CREATEMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_createmocompdata)

[**ProcAmpControlQueryCaps**](dxva-deinterlacecontainerdeviceclass-procampcontrolquerycaps.md)

[**ProcAmpControlQueryRange**](dxva-deinterlacecontainerdeviceclass-procampcontrolqueryrange.md)

 

 






