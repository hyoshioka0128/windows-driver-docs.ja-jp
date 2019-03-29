---
title: UVC 拡張ユニットのサンプル インターフェイス
description: UVC 拡張ユニットのサンプル インターフェイス
ms.assetid: 898fdaf7-c3e1-4ef5-be4e-a5f9849ee905
keywords:
- WDK USB ビデオ クラスのインターフェイス
- 拡張機能ユニット WDK USB ビデオ クラス、サンプル、インターフェイス
- サンプル コード UVC 拡張機能のユニットのインターフェイスの WDK USB ビデオ クラス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ad74a5c6da9bff231e71318b18f52aecb946fbe2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574105"
---
# <a name="sample-interface-for-uvc-extension-units"></a>UVC 拡張ユニットのサンプル インターフェイス


このトピックのサンプルについては、コードは*interface.idl*単位の拡張機能をサポートするために使用することできます。

```IDL
// IExtensionUnit interface
import "unknwn.idl";
[
   object,
   local,
   uuid(yyyyyyyy-yyyy-yyyy-yyyy-yyyyyyyyyyyy),
   pointer_default(unique)
]
interface IExtensionUnit : IUnknown
{
   HRESULT get_InfoSize(
      [out] ULONG *pulSize);
   HRESULT get_Info(
      [in] ULONG ulSize,
      [in, out, size_is(ulSize)] BYTE pInfo[]);
   HRESULT get_PropertySize(
      [in] ULONG PropertyId,
      [out] ULONG *pulSize);
 HRESULT get_Property(
      [in] ULONG PropertyId,
      [in] ULONG ulSize,
      [in, out, size_is(ulSize)] BYTE pValue[]);
   HRESULT put_Property(
      [in] ULONG PropertyId,
      [in] ULONG ulSize,
      [in, out, size_is(ulSize)] BYTE pValue[]);
   HRESULT get_PropertyRange(
      [in] ULONG PropertyId,
      [in] ULONG ulSize,
      [in, out, size_is(ulSize)] BYTE pMin[],
      [in, out, size_is(ulSize)] BYTE pMax[],
      [in, out, size_is(ulSize)] BYTE pSteppingDelta[],
      [in, out, size_is(ulSize)] BYTE pDefault[]);
};
```

 

 




