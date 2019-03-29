---
title: HS_DEVICE_IDENTITY 構造体
description: HS_DEVICE_IDENTITY 構造体には、デバイス モデルと製造元に関する情報が含まれています。
ms.assetid: 4a679fb2-d5b1-4635-9422-a21a316b360c
keywords:
- Windows Vista 以降のドライバーをネットワーク HS_DEVICE_IDENTITY 構造体
- Windows Vista 以降のドライバーをネットワーク PHS_DEVICE_IDENTITY 構造体ポインター
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe8a59888b032657a764bca0b7dfcfc0d763e79f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581543"
---
# <a name="hsdeviceidentity-structure"></a>HS\_デバイス\_IDENTITY 構造体

[!include[Wi-Fi Hotspot Offloading deprecation](wi-fi-hotspot-offloading-deprecation.md)]


**HS\_デバイス\_IDENTITY**構造体には、デバイス モデルと製造元に関する情報が含まれています。

<a name="syntax"></a>構文
------

```ManagedCPlusPlus
typedef struct _HS_DEVICE_IDENTITY {
  DWORD dwSystemType;
  WCHAR wszPhoneManufacturer[HS_CONST_MAX_DEVICE_INFO_LENGTH+1];
  WCHAR wszPhoneModelName[HS_CONST_MAX_DEVICE_INFO_LENGTH+1];
  WCHAR wszPhoneManufacturerModel[HS_CONST_MAX_DEVICE_INFO_LENGTH+1];
  WCHAR wszDeviceModel[HS_CONST_MAX_DEVICE_INFO_LENGTH+1];
} HS_DEVICE_IDENTITY, *PHS_DEVICE_IDENTITY;
```

<a name="members"></a>メンバー
-------

**dwSystemType**  
SIM の型かどうか、GSM または CDMA します。

**wszPhoneManufacturer**  
電話の製造元の名前です。

**wszPhoneModelName**  
電話のモデル名。

**wszPhoneManufacturerModel**  
電話の製造元とモデルの別の名前。

**wszDeviceModel**  
デバイス モデルの名前。

<a name="requirements"></a>必要条件
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Hotspotoffloadplugin.h (Hotspotoffloadplugin.h を含む)</td>
</tr>
</tbody>
</table>

 

 




