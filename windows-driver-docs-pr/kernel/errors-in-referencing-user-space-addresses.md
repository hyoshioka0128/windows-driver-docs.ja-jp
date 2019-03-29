---
title: ユーザー領域のアドレス参照エラー
description: ユーザー領域のアドレス参照エラー
ms.assetid: 87944805-e4ba-431e-b673-b0125dc9ec24
keywords:
- 信頼性 WDK カーネルでは、ユーザー空間アドレス
- WDK のカーネルを参照しているユーザー空間アドレス
- ユーザー領域のアドレスを参照します。
- 埋め込みポインター WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e21689350241f805401a639a3047b7e9d48e2937
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570580"
---
# <a name="errors-in-referencing-user-space-addresses"></a>ユーザー領域のアドレス参照エラー





任意のドライバーでは、これを使用する前にユーザー領域で任意のアドレスを検証する必要がありますは、Irp または高速の I/O 操作をサポートしているかどうか。 I/O マネージャーは、このようなアドレスは検証されません。 またドライバーに渡されたバッファーに埋め込まれているポインターは検証。

### <a href="" id="failure-to-validate-addresses-passed-in-method-neither-ioctls-and-fsctls"></a>メソッドに渡されたアドレスの検証に失敗した\_NEITHER Ioctl と FSCTLs

I/O マネージャーには、検証は行われませんメソッドに一切\_も Ioctl と FSCTLs します。 ユーザー スペースの住所が有効なことに、ドライバーを使用する必要があります、 [ **ProbeForRead** ](https://msdn.microsoft.com/library/windows/hardware/ff559876)と[ **ProbeForWrite** ](https://msdn.microsoft.com/library/windows/hardware/ff559879)ルーチン内のすべてのバッファー参照を囲む**試用/を除く**ブロックします。

次の例では、ドライバーに渡される値前提としています、 **Type3InputBuffer**有効なアドレスを表します。

```cpp
   case IOCTL_GET_HANDLER:
   {
      PULONG EntryPoint;

      EntryPoint =
         IrpSp->Parameters.DeviceIoControl.Type3InputBuffer; 
      *EntryPoint = (ULONG)DriverEntryPoint; 
      ...
   }
```

次のコードは、この問題を回避できます。

```cpp
   case IOCTL_GET_HANDLER:
   {
      PULONG_PTR EntryPoint;

      EntryPoint =
         IrpSp->Parameters.DeviceIoControl.Type3InputBuffer;
 
      try
      {
         if (Irp->RequestorMode != KernelMode)
         { 
            ProbeForWrite(EntryPoint,
                          sizeof(ULONG_PTR),
                          TYPE_ALIGNMENT(ULONG_PTR));
         }
         *EntryPoint = (ULONG_PTR)DriverEntryPoint;
      }
      except(EXCEPTION_EXECUTE_HANDLER)
      {
        ...
      }
      ...
   }
```

正しいコードがキャストにも注意してください**DriverEntryPoint** ULONG へ\_PTR、ULONG の代わりにします。 この変更で、64 ビットの Windows 環境で使用をできます。

### <a name="failure-to-validate-pointers-embedded-in-buffered-io-requests"></a>バッファー内の I/O 要求に埋め込まれているポインターの検証に失敗しました

多くの場合、ドライバーは、次の例のように、バッファー内の要求内のポインターを埋め込みます。

```cpp
   struct ret_buf
   {
      void  *arg;  // Pointer embedded in request
      int  rval;
   };

   pBuf = Irp->AssociatedIrp.SystemBuffer;
   ...
   arg = pBuf->arg;  // Fetch the embedded pointer
   ...
   // If the arg pointer is not valid, the following
   // statement can corrupt the system:
   RtlMoveMemory(arg, &info, sizeof(info));
```

この例で、ドライバーを使用して埋め込みポインターを検証する必要があります、**プローブ * Xxx*** で囲まれているルーチンを**試用/を除く**メソッドと同じ方法でブロック\_も Ioctl前に説明したようにします。 ポインターを埋め込むには、余分な情報を取得するためのドライバーができますが、ドライバーは相対的なオフセットまたは可変長バッファーを使用して、同じ結果をより効率的に得ることが。

使用しての詳細については**試用/を除く**、無効なアドレスを処理するためにブロックを参照してください[例外処理](handling-exceptions.md)します。

 

 




