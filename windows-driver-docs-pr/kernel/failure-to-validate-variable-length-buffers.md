---
title: 可変長バッファーを検証に失敗しました
description: 可変長バッファーを検証に失敗しました
ms.assetid: 0cc4be22-8197-421a-a5a6-2e7b89a79a38
keywords:
- 入力バッファーの WDK カーネル
- 入力バッファーの可変長の WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: be723319ea8d6b2419f40e83068f0e6d0e6f0bb6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56538663"
---
# <a name="failure-to-validate-variable-length-buffers"></a>可変長バッファーを検証に失敗しました





ドライバーは、固定ヘッダーと末尾の次の例のように、可変長のデータの入力バッファーを受け付けることがあります。

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

場合**WaitBuffer -&gt;NameLength**は整数のオーバーフローが起こる可能性のオフセットを追加する、非常に大きな ULONG 値です。 代わりに、ドライバーはオフセットを減算する必要があります、 **InputBufferLength**とで結果を比較**WaitBuffer -&gt;NameLength**、次の例。

```cpp
   if (InputBufferLength < sizeof(WAIT_FOR_BUFFER)) {
      IoCompleteRequest( Irp, STATUS_INVALID_PARAMETER );
      Return( STATUS_INVALID_PARAMETER );
   }

   WaitBuffer = Irp->AssociatedIrp.SystemBuffer;

   if ((InputBufferLength -
         FIELD_OFFSET(WAIT_FOR_BUFFER, Name[0])  >
         WaitBuffer->NameLength) {
      IoCompleteRequest( Irp, STATUS_INVALID_PARAMETER );
      return( STATUS_INVALID_PARAMETER );
   }
```

に、上記の減算がアンダー フローをできません最初**場合**ステートメントにより、 **InputBufferLength**のサイズ以上**待機\_の\_バッファー**します。

複雑なオーバーフロー問題を次に示します。

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

この例では、整数のオーバーフローを乗算中に発生します。 場合のサイズ、**設定\_値\_情報**構造体が 2 の倍数を**NumEntries**値のビットがときに、オーバーフロー 0x80000000 結果を中に左にシフトなど乗算します。 ただし、バッファー サイズはそれでも検証テストに合格、オーバーフローを引き起こします**dwSize**を非常に小さく表示されます。 この問題を避けるためには、前の例と長さを減算、除算**sizeof**(**設定\_値\_情報**) を使って結果を比較し、 **NumEntries**します。

 

 




