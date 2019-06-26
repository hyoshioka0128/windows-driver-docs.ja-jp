---
title: ProcAmpControlOpenStream メソッド
description: サンプルの DXVA\_ProcAmpControlDeviceClass::ProcAmpControlOpenStream 関数 ProcAmp ストリーム オブジェクトを作成します。
ms.assetid: 73011ce3-f643-4fca-bcfd-1467a9b56181
keywords:
- ディスプレイ デバイスの ProcAmpControlOpenStream メソッド
- ProcAmpControlOpenStream メソッド ディスプレイ デバイス、DXVA_ProcAmpControlDeviceClass インターフェイス
- DXVA_ProcAmpControlDeviceClass は、ProcAmpControlOpenStream メソッドのディスプレイ デバイスをインターフェイスします。
topic_type:
- apiref
api_name:
- DXVA_ProcAmpControlDeviceClass.ProcAmpControlOpenStream
api_type:
- COM
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: ceefb1472fc09c3c6f403c8e308e9c1deacaffa8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375816"
---
# <a name="dxvaprocampcontroldeviceclassprocampcontrolopenstream-method"></a>DXVA\_ProcAmpControlDeviceClass::ProcAmpControlOpenStream メソッド


サンプル*ProcAmpControlOpenStream*関数 ProcAmp ストリーム オブジェクトを作成します。

<a name="syntax"></a>構文
------

```cpp
HRESULT ProcAmpControlOpenStream(
  [in] LPDXVA_VideoDesc lpVideoDescription
);
```

<a name="parameters"></a>パラメーター
----------

*lpVideoDescription* \[で\]へのポインターを提供する[ **DXVA\_VideoDesc** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videodesc) ProcAmp の制御パラメーターを定義する構造体処理するビデオです。

<a name="return-value"></a>戻り値
------------

0 を返します (S\_[ok] または DD\_OK) 成功した場合、それ以外の場合、エラー コードを返します。 参照してください*ddraw.h*エラー コードの完全な一覧についてはします。

<a name="remarks"></a>注釈
-------

後に、 *VMR*が特定の機能と、ProcAmp ハードウェアを使用してコントロールの範囲、 [ **ProcAmpControlQueryCaps** ](dxva-deinterlacecontainerdeviceclass-procampcontrolquerycaps.md)と[ **ProcAmpControlQueryRange** ](dxva-deinterlacecontainerdeviceclass-procampcontrolqueryrange.md)関数、ProcAmp ストリーム オブジェクトを作成することができます。 ProcAmp ストリーム オブジェクトの作成は、ディスプレイ ドライバー ProcAmp 調整操作を実行するために必要なハードウェア リソースを予約できます。

*ProcAmpControlOpenStream*の CreateMoComp メンバーへの呼び出しに直接関数は、マップ、 [ **DD\_MOTIONCOMPCALLBACKS** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)構造体。 CreateMoComp メンバーが参照するドライバーによって提供される関数を指す、 [ **DD\_CREATEMOCOMPDATA** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_createmocompdata)構造体。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>参照してください。


[**DXVA\_VideoDesc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dxva/ns-dxva-_dxva_videodesc)

[**DD\_MOTIONCOMPCALLBACKS**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**DD\_CREATEMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_createmocompdata)

[**ProcAmpControlQueryCaps**](dxva-deinterlacecontainerdeviceclass-procampcontrolquerycaps.md)

[**ProcAmpControlQueryRange**](dxva-deinterlacecontainerdeviceclass-procampcontrolqueryrange.md)

 

 






