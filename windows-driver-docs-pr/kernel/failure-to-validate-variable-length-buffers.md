---
title: 可変長バッファーの検証失敗
description: 可変長バッファーの検証失敗
ms.assetid: 0cc4be22-8197-421a-a5a6-2e7b89a79a38
keywords:
- 入力バッファー WDK カーネル
- 可変長入力バッファー WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9497c5944dcf88bc301d2421b621967bf59bc34
ms.sourcegitcommit: 6e2986506940c203a6a834a927a774b7efa6b86e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/05/2020
ms.locfileid: "82800093"
---
# <a name="failure-to-validate-variable-length-buffers"></a>可変長バッファーの検証失敗





ドライバーは、次の例のように、固定ヘッダーと末尾の可変長データを含む入力バッファーを受け取ることがよくあります。

```cpp
   typedef struct _WAIT_FOR_BUFFER {
      LARGE_INTEGER Timeout;
      ULONG NameLength;
      BOOLEAN TimeoutSpecified;
      WCHAR Name[1];
   } WAIT_FOR_BUFFER, *PWAIT_FOR_BUFFER;

   if (InputBufferLength < sizeof(WAIT_FOR_BUFFER)) {
      IoCompleteRequest( Irp, STATUS_INVALID_PARAMETER );
      return( STATUS_INVALID_PARAMETER );
   }

   WaitBuffer = Irp->AssociatedIrp.SystemBuffer;

   if (FIELD_OFFSET(WAIT_FOR_BUFFER, Name[0]) +
          WaitBuffer->NameLength > InputBufferLength) {
       IoCompleteRequest( Irp, STATUS_INVALID_PARAMETER );
       return( STATUS_INVALID_PARAMETER );
   }
```

NameLength が非常に大きな ULONG 値である場合、それをオフセットに追加すると、整数オーバーフローが発生する可能性があります。 **&gt;** 代わりに、次の例に示すように、ドライバーは**Inputbufferlength** (buffer size) からオフセット (固定ヘッダーサイズ) を減算し、結果が**&gt;NameLength** (可変長データ) に対して十分な領域を残しているかどうかをテストする必要があります。

```cpp
   if (InputBufferLength < sizeof(WAIT_FOR_BUFFER)) {
      IoCompleteRequest( Irp, STATUS_INVALID_PARAMETER );
      Return( STATUS_INVALID_PARAMETER );
   }

   WaitBuffer = Irp->AssociatedIrp.SystemBuffer;

   if ((InputBufferLength -
         FIELD_OFFSET(WAIT_FOR_BUFFER, Name[0])  <
         WaitBuffer->NameLength) {
      IoCompleteRequest( Irp, STATUS_INVALID_PARAMETER );
      return( STATUS_INVALID_PARAMETER );
   }
```

つまり、バッファーサイズから固定ヘッダーサイズを引いた値が、可変長データに必要なバイト数よりも少ない場合、エラーが返されます。

最初の**if**ステートメントでは、 **inputbufferlength**が**\_BUFFER の\_待機**のサイズ以上であることが保証されるため、上記の減算はアンダーフローできません。

次に、より複雑なオーバーフローの問題を示します。

```cpp
   case IOCTL_SET_VALUE:
      dwSize = sizeof(SET_VALUE);

      if (inputBufferLength < dwSize) {
         ntStatus = STATUS_BUFFER_TOO_SMALL;
         break;
      }

      dwSize = FIELD_OFFSET(SET_VALUE, pInfo[0]) +
                  pSetValue->NumEntries * sizeof(SET_VALUE_INFO);

      if (inputBufferLength < dwSize) {
         ntStatus = STATUS_BUFFER_TOO_SMALL;
         break;
      }
```

この例では、乗算中に整数オーバーフローが発生する可能性があります。 **SET\_VALUE\_INFO**構造体のサイズが2の倍数の場合、0x80000000 のような**numentries**値はオーバーフローになり、乗算中にビットが左にシフトされます。 ただし、オーバーフローによって**dwSize**が非常に小さく表示されるため、バッファーサイズは検証テストに合格します。 この問題を回避するには、前の例のように長さを減算し、 **sizeof**(**値\_\_の設定**) で除算して、結果と**numentries**を比較します。

 

 




