---
title: EFI_USBFN_TRANSFER_STATUS
description: EFI_USBFN_TRANSFER_STATUS
ms.assetid: 60631dad-a617-4ed4-a975-5e480cf324e3
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4aa9b795c851f1bc958bf05a5eef0bdae43a9c0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337668"
---
# <a name="efiusbfntransferstatus"></a>EFI\_USBFN\_転送\_状態


この列挙体では、USB 転送状態を示します。

## <a name="syntax"></a>構文


```cpp
typedef enum _EFI_USBFN_TRANSFER_STATUS 
{
    UsbTransferStatusUnknown = 0,
    UsbTransferStatusComplete,
    UsbTransferStatusAborted,
    UsbTransferStatusActive,
    UsbTransferStatusNone
} EFI_USBFN_TRANSFER_STATUS;
```

## <a name="constants"></a>定数


<a href="" id="usbtransferstatusunknown"></a>**UsbTransferStatusUnknown**  
転送状態が不明です。

<a href="" id="usbtransferstatuscomplete"></a>**UsbTransferStatusComplete**  
転送を完了します。

<a href="" id="usbtransferstatusaborted"></a>**UsbTransferStatusAborted**  
転送が中止されました。

<a href="" id="usbtransferstatusactive"></a>**UsbTransferStatusActive**  
転送がアクティブです。

<a href="" id="usbtransferstatusnone"></a>**UsbTransferStatusNone**  
転送には、状態がありません。

## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

 

 




