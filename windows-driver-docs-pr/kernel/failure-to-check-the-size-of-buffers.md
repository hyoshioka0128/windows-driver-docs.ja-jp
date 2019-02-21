---
title: バッファーのサイズを確認するエラー
description: バッファーのサイズを確認するエラー
ms.assetid: e9d9a5d9-19a5-4a1d-95f9-df2021c51c41
keywords:
- バッファー サイズの WDK カーネル
- 入力バッファーの WDK カーネル
- 出力バッファーの WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2673d535c8b2d123e5fa6c53f8c9eaeac8583a2a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527969"
---
# <a name="failure-to-check-the-size-of-buffers"></a>バッファーのサイズを確認するエラー





Ioctl およびバッファー内の I/O を実装する FSCTLs を処理する際、ドライバーは、バッファーが要求されたすべてのデータを保持できることを確認する入力と出力バッファーのサイズを常に確認する必要があります。 要求がファイルを指定する場合\_ANY\_Ioctl と FSCTLs do、呼び出し元をデバイスを識別するハンドルを持つほとんどのドライバーが、そのデバイスのバッファー内の IOCTL または FSCTL 要求へのアクセスにアクセスし、でした読み取りまたは書き込みの末尾を越えるデータ、バッファー。

### <a name="input-buffer-size"></a>入力バッファーのサイズ

たとえば、呼び出し元であるルーチンで、次のコードが表示されることを*ディスパッチ*ルーチンと、ドライバーが IRP に渡されたバッファーのサイズに検証されていません。

```cpp
   switch (ControlCode)
      ...
      ...
      case IOCTL_NEW_ADDRESS:{
         tNEW_ADDRESS *pNewAddress = 
            pIrp->AssociatedIrp.SystemBuffer;

         pDeviceContext->Addr = RtlUlongByteSwap (pNewAddress->Address);
```

例では、(ハイライト表示)、代入ステートメントの前にバッファー サイズをチェックしません。 結果として、 **pNewAddress -&gt;アドレス**入力バッファーが、tNEW を格納するのに十分でない場合、次の行の参照はエラーことができます\_アドレス構造体。

次のコードは、バッファー サイズは、潜在的な問題を避けることを確認します。

```cpp
   case IOCTL_NEW_ADDRESS: {
      tNEW_ADDRESS *pNewAddress =
         pIrp->AssociatedIrp.SystemBuffer;

      if (pIrpSp->Parameters.DeviceIoControl.InputBufferLength >=
             sizeof(tNEW_ADDRESS)) {
         pDeviceContext->Addr = RtlUlongByteSwap (pNewAddress->Address);
```

可変サイズのバッファーを使用する WMI 要求などのバッファー内の他の I/O を処理するコードは、同様のエラーを持つことができます。

### <a name="output-buffer-size"></a>出力バッファーのサイズ

出力バッファーの問題は、入力バッファーの問題に似ています。 プールを破損することが簡単にして、ユーザー モードの呼び出し元にエラーが発生したことを認識できない可能性があります。

次の例では、ドライバーに失敗のサイズを確認する、 **SystemBuffer**:

```cpp
   case IOCTL_GET_INFO: {

       Info = Irp->AssociatedIrp.SystemBuffer;

       Info->NumIF = NumIF;
       ...
       ...
       Irp->IoStatus.Information =
             NumIF*sizeof(GET_INFO_ITEM)+sizeof(ULONG);
       Irp->IoStatus.Status = ntStatus;
   }
```

仮定すると、 **NumIF**システム バッファーのフィールドが入力項目の数を指定し、この例を設定できる、 **IoStatus.Information**出力よりも大きな値をバッファーし、多すぎるため返しますユーザー モード コードの情報です。 アプリケーションが正しくコード化された「小さすぎて出力バッファーが、上記のコードの呼び出しは、システム バッファーの末尾を越えて書き込みによって、プールを破損する可能性がある場合は。

I/O マネージャーが想定することに注意してください。 の値、**情報**フィールドは有効です。 呼び出し元は、出力バッファーのサイズが 0 バイトのカーネル モードの有効なアドレスでは、ドライバーからの出力バッファー サイズを確認して、エラーを見つけるためしなかった場合、深刻な問題が発生することができます。

 

 




