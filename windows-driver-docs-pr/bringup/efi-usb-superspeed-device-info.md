---
title: EFI_USB_SUPERSPEED_DEVICE_INFO
description: EFI_USB_SUPERSPEED_DEVICE_INFO
ms.assetid: 7861BA16-7499-48A1-9D6A-9BB8F5AA36CE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f2bcc9909d7cc666164b80e737d2b2b74f6afdb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337746"
---
# <a name="efiusbsuperspeeddeviceinfo"></a>EFI\_USB\_SUPERSPEED\_デバイス\_情報


**EFI\_USB\_SUPERSPEED\_デバイス\_情報**USB SuperSpeed 関数デバイスを定義する構造を使用します。

## <a name="syntax"></a>構文


```cpp
typedef struct 
{
    EFI_USB_DEVICE_DESCRIPTOR           *DeviceDescriptor;
    EFI_USB_SUPERSPEED_CONFIG_INFO      **ConfigInfoTable;
    EFI_USB_BOS_DESCRIPTOR              *BosDescriptor
} EFI_USB_SUPERSPEED_DEVICE_INFO;
```

## <a name="members"></a>メンバー


<a href="" id="devicedescriptor"></a>**DeviceDescriptor**  
EFI\_USB\_デバイス\_USB デバイスの構成情報を含む記述子構造体。

<a href="" id="configinfotable"></a>**ConfigInfoTable**  
[EFI\_USB\_SUPERSPEED\_CONFIG\_情報](efi-usb-superspeed-config-info.md)USB SuperSpeed でサポートされる構成に関する情報を含む構造体。

<a href="" id="bosdescriptor"></a>**BosDescriptor**  
[EFI\_USB\_BOS\_記述子](efi-usb-bos-descriptor.md)USB 機能ドライバーをバイナリ オブジェクト ストアに関する情報を含む構造体。

## <a name="remarks"></a>注釈


**EFI\_USB\_CONFIG\_記述子**構造体は、UEFI 仕様バージョン 2.3 で定義されている以降。 詳細については、次を参照してください。、 [UEFI.org](https://go.microsoft.com/fwlink/p/?linkid=109526) web サイト。

## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

 

 




