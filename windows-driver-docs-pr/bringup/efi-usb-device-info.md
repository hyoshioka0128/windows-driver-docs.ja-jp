---
title: EFI_USB_DEVICE_INFO
description: EFI_USB_DEVICE_INFO
ms.assetid: b44f77fc-f496-488f-b53a-b54420da9360
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 79fb8ed527c791ac5b5dcdeae77172ee4cd796e7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337807"
---
# <a name="efiusbdeviceinfo"></a>EFI\_USB\_デバイス\_情報


**EFI\_USB\_デバイス\_情報**構造を使用して関数の USB デバイスを定義します。

## <a name="syntax"></a>構文


```cpp
typedef struct 
{
    EFI_USB_DEVICE_DESCRIPTOR           *DeviceDescriptor;
    EFI_USB_CONFIG_INFO                 **ConfigInfoTable;
} EFI_USB_DEVICE_INFO;
```

## <a name="members"></a>メンバー


<a href="" id="devicedescriptor"></a>**DeviceDescriptor**  
EFI\_USB\_デバイス\_USB デバイスの構成情報を含む記述子構造体。

<a href="" id="configinfotable"></a>**ConfigInfoTable**  
EFI\_USB\_CONFIG\_でサポートされる構成に関する情報を含む情報構造体。

## <a name="remarks"></a>注釈


**EFI\_USB\_CONFIG\_記述子**と**EFI\_USB\_デバイス\_記述子**構造が定義されています。UEFI 仕様 2.3 します。 詳細については、次を参照してください。、 [UEFI.org](https://go.microsoft.com/fwlink/p/?linkid=109526) web サイト。

## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

 

 




