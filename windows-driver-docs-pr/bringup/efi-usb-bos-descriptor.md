---
title: EFI_USB_BOS_DESCRIPTOR
description: EFI_USB_BOS_DESCRIPTOR
ms.assetid: A12E3678-E5B6-4AB0-8F28-FCDA57C9D397
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: deb849b3b17e57852134e697e4a50d798bea5b11
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575021"
---
# <a name="efiusbbosdescriptor"></a>EFI\_USB\_BOS\_記述子


**EFI\_USB\_BOS\_記述子**構造体は、USB 機能ドライバーをバイナリ オブジェクト ストア (BOS) についての情報を提供します。

## <a name="syntax"></a>構文


```cpp
typedef struct
{
    UINT8   Length;
    UINT8   DescriptorType;
    UINT16  TotalLength;
    UINT8   NumDeviceCaps;
} EFI_USB_BOS_DESCRIPTOR;
```

## <a name="members"></a>メンバー


<a href="" id="length"></a>**長さ**  
記述子のサイズ。

<a href="" id="descriptortype"></a>**DescriptorType**  
BOS 記述子の型。

<a href="" id="totallength"></a>**TotalLength**  
この記述子およびすべてのサブ記述子の長さ。

<a href="" id="numdevicecaps"></a>**NumDeviceCaps**  
BOS 内の別のデバイス機能の記述子の数。

## <a name="requirements"></a>必要条件


**ヘッダー:** ユーザーが生成しました。

 

 




