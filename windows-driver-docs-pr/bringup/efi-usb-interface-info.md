---
title: EFI_USB_INTERFACE_INFO
description: EFI_USB_INTERFACE_INFO
ms.assetid: d20b78bd-8369-4f50-b161-e8ad0bb4c52f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8af735b385de3b47075f1eebf938a2129c902991
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337762"
---
# <a name="efiusbinterfaceinfo"></a>EFI\_USB\_インターフェイス\_情報


**EFI\_USB\_インターフェイス\_情報**サポートされている USB インターフェイスを定義するには、使用されている構造体します。

## <a name="syntax"></a>構文


```cpp
typedef struct 
{
    EFI_USB_INTERFACE_DESCRIPTOR        *InterfaceDescriptor;
    EFI_USB_ENDPOINT_DESCRIPTOR         **EndpointDescriptorTable;
} EFI_USB_INTERFACE_INFO;
```

## <a name="members"></a>メンバー


<a href="" id="interfacedescriptor"></a>**InterfaceDescriptor**  
EFI\_USB\_インターフェイス\_USB 関数インターフェイスに関する情報を含む記述子構造体。 参照してください**解説**します。

<a href="" id="endpointdescriptortable"></a>**EndpointDescriptorTable**  
EFI\_USB\_エンドポイント\_サポートされているエンドポイントに関する情報を含む記述子構造体。 参照してください**解説**します。

## <a name="remarks"></a>注釈


**USB\_インターフェイス\_記述子**と**USB\_エンドポイント\_記述子**構造体は、UEFI 仕様 2.3 で定義されます。 詳細については、次を参照してください。、 [UEFI.org](https://go.microsoft.com/fwlink/p/?linkid=109526) web サイト。

## <a name="requirements"></a>必要条件


**ヘッダー:** ユーザーが生成しました。

 

 




