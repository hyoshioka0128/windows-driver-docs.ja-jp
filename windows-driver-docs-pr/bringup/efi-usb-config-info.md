---
title: EFI_USB_CONFIG_INFO
description: EFI_USB_CONFIG_INFO
ms.assetid: 74d5cb02-2648-4bd1-990e-61156b5dc8cd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7db5cab0dc38e26f692b13f69f52e47c277ec9d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337787"
---
# <a name="efiusbconfiginfo"></a>EFI\_USB\_CONFIG\_情報


**EFI\_USB\_CONFIG\_情報**構造を使用して、サポートされている USB ポートの構成を定義します。

## <a name="syntax"></a>構文


```cpp
typedef struct 
{
    EFI_USB_CONFIG_DESCRIPTOR           *ConfigDescriptor;
    EFI_USB_INTERFACE_INFO              **InterfaceInfoTable;
} EFI_USB_CONFIG_INFO;
```

## <a name="members"></a>メンバー


<a href="" id="configdescriptor"></a>**ConfigDescriptor**  
EFI\_USB\_CONFIG\_関数の USB デバイスの構成情報を含む記述子構造体。

<a href="" id="interfaceinfotable"></a>**InterfaceInfoTable**  
[EFI\_USB\_インターフェイス\_情報](efi-usb-interface-info.md)サポートされているインターフェイスに関する情報を含む構造体。

## <a name="remarks"></a>注釈


構造体**USB\_CONFIG\_記述子**2.3 の UEFI 仕様で定義されています。 詳細については、次を参照してください。、 [UEFI.org](https://go.microsoft.com/fwlink/p/?linkid=109526) web サイト。

## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

 

 




