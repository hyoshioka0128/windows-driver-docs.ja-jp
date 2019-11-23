---
title: I/O 制御コードの定義
description: I/O 制御コードの定義
ms.assetid: 967b0199-e9a0-4c8d-9130-c81436c59ca3
keywords:
- I/o 制御コード WDK カーネル、定義
- コントロールコード WDK Ioctl、定義
- Ioctl WDK カーネル、定義
- CTL_CODE マクロ
- Ioctl WDK ユーザーモード
- ユーザーモードコンポーネント WDK Ioctl
- I/o 制御コード WDK ユーザーモード
- コントロールコード WDK ユーザーモード
- レイアウト WDK Ioctl
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e2717c85abad25fb68011b0d497d2005c9c8f04
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72828423"
---
# <a name="defining-io-control-codes"></a>I/O 制御コードの定義





新しい Ioctl を定義するときは、次の規則に注意することが重要です。

-   ユーザーモードのソフトウェアコンポーネントが新しい IOCTL を使用できるようにするには、IOCTL を[**IRP\_MJ\_デバイス\_制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)要求と共に使用する必要があります。 ユーザーモードコンポーネントは、Win32 関数である[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)を呼び出すことによって、 **IRP\_MJ\_デバイス\_制御**要求を送信します。
-   新しい IOCTL をカーネルモードドライバーコンポーネントのみで使用できるようにするには、IOCTL を[**IRP\_MJ\_内部\_デバイス\_制御**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-internal-device-control)要求で使用する必要があります。 カーネルモードコンポーネントは、 **IoBuildDeviceIoControlRequest**を呼び出すことによって、**内部\_デバイス\_制御要求を\_\_IRP MJ**を作成します。 詳細については、「[ドライバーで IOCTL 要求を作成する](creating-ioctl-requests-in-drivers.md)」を参照してください。

I/o 制御コードは、複数のフィールドで構成される32ビット値です。 次の図は、i/o 制御コードのレイアウトを示しています。

![i/o 制御コードレイアウトを示す図](images/ioctl-1.png)

Ntddk およびで定義されているシステム指定の**CTL\_コード**マクロを使用して、新しい i/o 制御コードを定義します。 新しい IOCTL コードの定義は、 **IRP\_\_MJ**での使用を意図しているかどうかにかかわらず、デバイス\_コントロールまたは**irp\_MJ\_内部\_デバイス\_コントロール**要求で使用することを想定して、次の形式を使用します。

```cpp
#define IOCTL_Device_Function CTL_CODE(DeviceType, Function, Method, Access)
```

Ioctl のわかりやすい定数名を選択します。 ioctl\_*device*\_*function*という形式*で指定します。 device は*デバイスの種類を示し、*関数*は操作を示します。 定数名の例としては、\_カーソルを有効にするビデオ\_\_があります。

**CTL\_コード**マクロに次のパラメーターを指定します。

<a href="" id="devicetype"></a> *(Devicetype*  
デバイスの種類を識別します。 この値は、ドライバーの[**デバイス\_オブジェクト**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)構造の **(devicetype**メンバーに設定されている値と一致する必要があります。 (「[デバイスの種類の指定」を](specifying-device-types.md)参照してください)。 0x8000 未満の値は、Microsoft 用に予約されています。 ベンダーは、0x8000 以上の値を使用できます。 ベンダーによって割り当てられた値によって**共通**ビットが設定されることに注意してください。

<a href="" id="functioncode"></a>*FunctionCode*  
ドライバーによって実行される関数を識別します。 0x800 未満の値は、Microsoft 用に予約されています。 0x800 以上の値は、ベンダーが使用できます。 ベンダーによって割り当てられた値によって**カスタム**ビットが設定されることに注意してください。

<a href="" id="transfertype"></a>*TransferType*  
システムが[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol) (または[**IoBuildDeviceIoControlRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)) の呼び出し元と IRP を処理するドライバーの間でデータを渡す方法を示します。

次のシステム定義定数のいずれかを使用します。

<a href="" id="method-buffered"></a>メソッド\_バッファーされる  
バッファーされた[i/o](methods-for-accessing-data-buffers.md)メソッドを指定します。通常は、要求ごとに少量のデータを転送するために使用されます。 デバイスと中間ドライバーの i/o 制御コードのほとんどは、この*Transfertype*値を使用します。

メソッド\_バッファー i/o 制御コードのデータバッファーを指定する方法については、「 [I/o 制御コードのバッファーの説明](buffer-descriptions-for-i-o-control-codes.md)」を参照してください。

バッファーされた i/o の詳細については、「[バッファー i/o の使用](using-buffered-i-o.md)」を参照してください。

<a href="" id="method-in-direct-or-method-out-direct"></a>\_直接またはメソッドでのメソッド\_\_OUT\_DIRECT  
[ダイレクト i/o](methods-for-accessing-data-buffers.md)方式を指定します。この方法は、通常、DMA または PIO を使用して大量のデータの読み取りや書き込みを行う場合に使用します。これは、迅速に転送する必要があります。

[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)または**IoBuildDeviceIoControlRequest**の呼び出し元がデータをドライバーに渡す場合は、\_DIRECT でメソッド\_を指定します。

[**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)または**IoBuildDeviceIoControlRequest**の呼び出し元がドライバーからデータを受信する場合は、メソッド\_OUT\_DIRECT に指定します。

システムでメソッドのデータバッファーを指定する方法の詳細については\_ダイレクト i/o 制御コードの\_OUT\_ダイレクト i/o 制御コードの\_を参照してください。 [I/o 制御コードのバッファーの説明](buffer-descriptions-for-i-o-control-codes.md)を参照してください。

ダイレクト i/o の詳細については、「 [direct i/o の使用](using-direct-i-o.md)」を参照してください。

<a href="" id="method-neither"></a>メソッド\_ません。  
[バッファーも直接 i/o も](using-neither-buffered-nor-direct-i-o.md)指定しません。 I/o マネージャーでは、システムバッファーや MDLs は提供されません。 IRP は、 [**DeviceIoControl**](https://docs.microsoft.com/windows/desktop/api/ioapiset/nf-ioapiset-deviceiocontrol)または**IoBuildDeviceIoControlRequest**に指定された入力バッファーと出力バッファーのユーザーモード仮想アドレスを、検証やマッピングを行わずに提供します。

I/o 制御コードでも\_メソッドのデータバッファーを指定する方法の詳細については、「 [I/o 制御コードのバッファーの説明](buffer-descriptions-for-i-o-control-codes.md)」を参照してください。

このメソッドは、ドライバーが i/o 制御要求を発信したスレッドのコンテキストで実行されていることを保証できる場合にのみ使用できます。 最上位レベルのカーネルモードドライバーのみがこの条件を満たしていることが保証されるため、メソッド\_、低レベルのデバイスドライバーに渡される i/o 制御コードにはほとんど使用されません。

このメソッドでは、最上位レベルのドライバーで、要求の受信時にバッファーまたはユーザーデータへの直接アクセスを設定するかどうかを決定する必要があります。また、ユーザーバッファーをロックダウンする必要があり、構造化例外ハンドラーでユーザーバッファーへのアクセスをラップする必要があります (「[例外の処理](handling-exceptions.md)」を参照)。 それ以外の場合、元のユーザーモードの呼び出し元は、ドライバーが使用できるようになる前にバッファー内のデータを変更したり、ドライバーがユーザーバッファーにアクセスしたときと同じように呼び出し元を交換したりすることができます。

詳細については、「[バッファーと直接 i/o の両方を使用する](using-neither-buffered-nor-direct-i-o.md)」を参照してください。

<a href="" id="requiredaccess"></a>*RequiredAccess*  
デバイスを表すファイルオブジェクトを開くときに、呼び出し元が要求するアクセスの種類を示します (「 [**IRP\_MJ\_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-create))」を参照してください。 I/o マネージャーは、Irp を作成し、呼び出し元が指定されたアクセス権を要求した場合にのみ、特定の i/o 制御コードを使用してドライバーを呼び出します。 *Requiredaccess*は、次のシステム定義定数を使用して指定します。

<a href="" id="file-any-access"></a>ファイル\_\_アクセス  
I/o マネージャーは、ターゲットデバイスオブジェクトを表すファイルオブジェクトへのハンドルを持つ任意の呼び出し元に対して、IRP を送信します。

<a href="" id="file-read-data"></a>ファイル\_読み取り\_データ  
I/o マネージャーは、読み取りアクセス権を持つ呼び出し元に対してのみ IRP を送信します。これにより、基になるデバイスドライバーは、デバイスからシステムメモリにデータを転送できます。

<a href="" id="file-write-data"></a>ファイル\_\_データを書き込む  
I/o マネージャーは、書き込みアクセス権を持つ呼び出し元に対してのみ IRP を送信します。これにより、基になるデバイスドライバーがシステムメモリからデバイスにデータを転送できるようになります。

呼び出し元が読み取りと書き込みの両方のアクセス権を持つ必要がある場合は、ファイル\_読み取り\_データおよびファイル\_書き込み\_データを書き込むことができます。

システムで定義された i/o 制御コードの中には、\_ファイルの*requiredaccess*値\_アクセス権があります。これにより、呼び出し元は、デバイスに付与されたアクセス権に関係なく、特定の IOCTL を送信できます。 たとえば、*排他的なデバイス*のドライバーに送信される i/o 制御コードがこれに含まれます。

システムによって定義されたその他の i/o 制御コードでは、呼び出し元に読み取りアクセス権、書き込みアクセス権、またはその両方を与える必要があります。 たとえば、次のようなパブリック i/o 制御\_コードの定義では、ディスク\_設定\_パーティション\_情報は、呼び出し元が読み取りと書き込みの両方のアクセス権を持っている場合にのみ、この i/o 要求がドライバーに送信されることを示しています。

```cpp
#define IOCTL_DISK_SET_PARTITION_INFO\
        CTL_CODE(IOCTL_DISK_BASE, 0x008, METHOD_BUFFERED,\
        FILE_READ_DATA | FILE_WRITE_DATA)
```

**注**   新しい IOCTL コードに\_アクセスする場合は、ファイル\_指定する前に、デバイスへの無制限のアクセスを許可しても、悪意のあるユーザーがシステムを危険にさらす可能性のあるパスを作成しないようにする必要があります。

 

ドライバーは、 [**IoValidateDeviceIoControlAccess**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iovalidatedeviceiocontrolaccess)を使用して、IOCTL の*requiredaccess*ビットによって提供されるより厳しいアクセスチェックを実行できます。

## <a name="other-useful-macros"></a>その他の便利なマクロ


次のマクロは、IOCTL コードから16ビットの *(devicetype*および2ビットの*transfertype*フィールドを抽出する場合に役立ちます。

```cpp
#define DEVICE_TYPE_FROM_CTL_CODE(ctrlCode)   (((ULONG)(ctrlCode & 0xffff0000)) >> 16)
#define METHOD_FROM_CTL_CODE(ctrlCode)        ((ULONG)(ctrlCode & 3))
```

これらのマクロは、Wdm および Ntddk で定義されています。

 

 




