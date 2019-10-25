---
title: ユーザー領域のアドレスを参照中のエラー
description: ユーザー領域のアドレスを参照中のエラー
ms.assetid: 87944805-e4ba-431e-b673-b0125dc9ec24
keywords:
- 信頼性 WDK カーネル、ユーザー領域のアドレス
- WDK カーネルを参照するユーザー領域のアドレス
- 参照元のユーザースペースアドレス
- 埋め込みポインター WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6bbfb7269f4aab1f97059fc28a15cb86a2aa975
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838705"
---
# <a name="errors-in-referencing-user-space-addresses"></a>ユーザー領域のアドレスを参照中のエラー





Irp をサポートするか、高速 i/o 操作であるかにかかわらず、すべてのドライバーは、使用を試みる前にユーザー領域内のアドレスを検証する必要があります。 I/o マネージャーでは、このようなアドレスは検証されません。また、ドライバーに渡されたバッファーに埋め込まれているポインターも検証されません。

### <a href="" id="failure-to-validate-addresses-passed-in-method-neither-ioctls-and-fsctls"></a>メソッドで渡されたアドレスを検証できませんでした\_Ioctl と FSCTLs のいずれでもありません

I/o マネージャーでは、Ioctl と FSCTLs のどちらのメソッド\_も検証は行われません。 ユーザースペースアドレスが有効であることを確認するには、ドライバーは、 **try/except**ブロック内のすべてのバッファー参照を含む[**ProbeForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforread)ルーチンと[**ProbeForWrite**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-probeforwrite)ルーチンを使用する必要があります。

次の例では、ドライバーは、 **Type3InputBuffer**に渡された値が有効なアドレスを表していると想定しています。

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

次のコードを実行すると、この問題が回避されます。

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

また、正しいコードによって、 **Driverentrypoint**が ulong ではなく\_PTR にキャストされることにも注意してください。 この変更により、64ビットの Windows 環境でを使用できるようになります。

### <a name="failure-to-validate-pointers-embedded-in-buffered-io-requests"></a>バッファーされた i/o 要求に埋め込まれたポインターを検証できませんでした

多くの場合、ドライバーは、次の例に示すように、バッファー内の要求内にポインターを埋め込みます。

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

この例では、ドライバーは、 **try/except**ブロックで囲まれた**プローブ * Xxx*** ルーチンを使用して、埋め込みポインターを検証する必要があります。これは、メソッドの場合と同じように、前に説明した ioctl\_ません。 ドライバーは、ポインターを埋め込むことによって追加情報を返すことができますが、相対オフセットまたは可変長バッファーを使用することにより、同じ結果を効率的に得ることができます。

**Try/except**ブロックを使用して無効なアドレスを処理する方法の詳細については、「[例外の処理](handling-exceptions.md)」を参照してください。

 

 




