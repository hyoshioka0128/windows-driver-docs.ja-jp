---
title: EFI_USBFN_TRANSFER_RESULT
description: EFI_USBFN_TRANSFER_RESULT
ms.assetid: d101b061-2a83-4bf8-9502-ccb6e56f5cea
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0267bdc76cdd0cfeefc3bcdeb1b164686bdcfd3d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56536167"
---
# <a name="efiusbfntransferresult"></a>EFI\_USBFN\_転送\_結果


**EFI\_USBFN\_転送\_結果**構造に転送またはホストから受信したデータに関する情報が含まれています。

## <a name="syntax"></a>構文


```cpp
typedef struct _EFI_USBFN_TRANSFER_RESULT 
{
    UINTN                         BytesTransferred;
    EFI_USBFN_TRANSFER_STATUS     TransferStatus;
    UINT8                         EndpointIndex;
    EFI_USBFN_ENDPOINT_DIRECTION  Direction;
    VOID                          *Buffer;
} EFI_USBFN_TRANSFER_RESULT;
```

## <a name="members"></a>Members


<a href="" id="bytestransferred"></a>**bytesTransferred**  
データの量は、バイト単位で転送されます。

<a href="" id="transferstatus"></a>**TransferStatus**  
型の列挙体[EFI\_USBFN\_転送\_状態](efi-usbfn-transfer-status.md)転送の状態を示します。

<a href="" id="endpointindex"></a>**EndpointIndex**  
通知が発生したエンドポイントのインデックス。

<a href="" id="direction"></a>**方向**  
エンドポイントの方向です。

<a href="" id="buffer"></a>**バッファー**  
転送されたデータを格納するバッファー。

## <a name="requirements"></a>要件


**ヘッダー:** ユーザーが生成しました。

 

 




