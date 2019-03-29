---
title: EFI_USB_CONFIG_INFO
description: EFI_USB_CONFIG_INFO
ms.assetid: 74d5cb02-2648-4bd1-990e-61156b5dc8cd
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7db5cab0dc38e26f692b13f69f52e47c277ec9d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571749"
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

## <a name="remarks"></a>コメント


構造体**USB\_CONFIG\_記述子**2.3 の UEFI 仕様で定義されています。 詳細については、次を参照してください。、 [UEFI.org](https://go.microsoft.com/fwlink/p/?linkid=109526) web サイト。

## <a name="requirements"></a>必要条件


**ヘッダー:** ユーザーが生成しました。

 

 




