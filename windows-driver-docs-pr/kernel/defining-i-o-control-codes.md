---
title: I/O 制御コードの定義
description: I/O 制御コードの定義
ms.assetid: 967b0199-e9a0-4c8d-9130-c81436c59ca3
keywords:
- I/O 制御コード WDK のカーネルを定義します。
- 制御コードを定義する、WDK の Ioctl
- Ioctl WDK のカーネルを定義します。
- CTL_CODE マクロ
- Ioctl WDK ユーザー モード
- ユーザー モード コンポーネント WDK Ioctl
- I/O 制御コード WDK ユーザー モード
- 制御コード WDK ユーザー モード
- WDK の Ioctl のレイアウト
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d7a39ed0d7b80cef7896f75d27f7b206cad137c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388279"
---
# <a name="defining-io-control-codes"></a>I/O 制御コードの定義





新しい Ioctl を定義するときに、次の規則に注意してください。

-   ユーザー モード ソフトウェア コンポーネントで使用できる新しい IOCTL 場合で、IOCTL を使用する必要があります[ **IRP\_MJ\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550744)要求。 ユーザー モード コンポーネント送信**IRP\_MJ\_デバイス\_コントロール**呼び出すことによって要求、 [ **DeviceIoControl**](https://msdn.microsoft.com/library/windows/desktop/aa363216)、これは、Win32 関数。
-   IOCTL で使用する必要がありますカーネル モード ドライバー コンポーネントにのみ使用可能な新しい IOCTL では場合、 [ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550766)要求。 カーネル モード コンポーネント作成**IRP\_MJ\_内部\_デバイス\_コントロール**を呼び出して要求**IoBuildDeviceIoControlRequest**します。 詳細については、次を参照してください。[ドライバー IOCTL 要求を作成する](creating-ioctl-requests-in-drivers.md)します。

I/O の制御コードは、いくつかのフィールドで構成される 32 ビット値です。 次の図は、I/O 制御コードのレイアウトを示します。

![i/o 制御コードのレイアウトを示す図](images/ioctl-1.png)

システム提供の使用**CTL\_コード**マクロで、新しい I/O 制御コードを定義するには、Wdm.h および Ntddk.h で定義されています。 新しい IOCTL の定義をコードで使用するためのものかどうか**IRP\_MJ\_デバイス\_コントロール**または**IRP\_MJ\_内部\_デバイス\_コントロール**要求、次の形式が使用されます。

```cpp
#define IOCTL_Device_Function CTL_CODE(DeviceType, Function, Method, Access)
```

フォーム IOCTL の IOCTL のわかりやすい定数名を選択\_*デバイス*\_*関数*ここで、*デバイス*の種類を示しますデバイスと*関数*操作を示します。 例の定数名は、IOCTL\_ビデオ\_を有効にする\_カーソル。

次のパラメーターを指定、 **CTL\_コード**マクロ。

<a href="" id="devicetype"></a>*DeviceType*  
デバイスの種類を識別します。 この値に設定されている値と一致する必要があります、 **DeviceType**のドライバーのメンバー [**デバイス\_オブジェクト**](https://msdn.microsoft.com/library/windows/hardware/ff543147)構造体。 (を参照してください[デバイスの種類を指定する](specifying-device-types.md))。 0x8000 未満の値は、Microsoft の予約されています。 0x8000 以降の値は、ベンダーで使用できます。 仕入先によって割り当てられた値の設定に注意してください、**共通**ビット。

<a href="" id="functioncode"></a>*FunctionCode*  
ドライバーで実行される関数を識別します。 Microsoft では、0x800 未満の値は予約されます。 0x800 以降の値は、ベンダーで使用できます。 仕入先によって割り当てられた値の設定に注意してください、**カスタム**ビット。

<a href="" id="transfertype"></a>*TransferType*  
システムが、呼び出し元の間でデータを渡す方法を示します[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216) (または[ **IoBuildDeviceIoControlRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548318)) とこのドライバーは IRP を処理します。

次のシステム定義の定数のいずれかを使用します。

<a href="" id="method-buffered"></a>メソッド\_バッファーに格納されました。  
指定します、 [I/O バッファー](methods-for-accessing-data-buffers.md)メソッドは、少量のデータを 1 回の要求を転送するために使われます。 デバイスとドライバーの中間のほとんどの I/O 制御コードを使用してこの*TransferType*値。

システムがメソッドのデータ バッファーを指定する方法については\_バッファー I/O 制御コードを参照してください[I/O 制御コードの説明をバッファー](buffer-descriptions-for-i-o-control-codes.md)します。

バッファー内の I/O の詳細については、次を参照してください。[を使用してバッファー I/O](using-buffered-i-o.md)します。

<a href="" id="method-in-direct-or-method-out-direct"></a>メソッド\_IN\_ダイレクトまたはメソッド\_アウト\_ダイレクト  
指定します、[ダイレクト I/O](methods-for-accessing-data-buffers.md)メソッドは、通常、読み取りまたは書き込み DMA または PIO、すばやく転送する必要がありますを使用して、データの大量に使用します。

メソッドを指定\_IN\_ダイレクトの場合、呼び出し元の[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)または**IoBuildDeviceIoControlRequest**ドライバーにデータを渡します。

メソッドを指定\_アウト\_ダイレクトの場合、呼び出し元の[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)または**IoBuildDeviceIoControlRequest**からデータを取得する、ドライバー。

システムがメソッドのデータ バッファーを指定する方法については\_IN\_ダイレクトとメソッド\_アウト\_ダイレクト I/O 制御コードを参照してください[I/O 制御コードバッファー説明](buffer-descriptions-for-i-o-control-codes.md).

ダイレクト I/O の詳細については、次を参照してください。[を使用して直接 I/O](using-direct-i-o.md)します。

<a href="" id="method-neither"></a>メソッド\_NEITHER  
指定します[バッファーも直接 I/O](using-neither-buffered-nor-direct-i-o.md)します。 I/O マネージャーでは、任意のシステムのバッファーまたは MDLs は提供されません。 IRP が提供するために指定された入力と出力バッファーのユーザー モード仮想アドレス[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)または**IoBuildDeviceIoControlRequest**、検証またはマッピングすることです。

システムがメソッドのデータ バッファーを指定する方法については\_も I/O 制御コードを参照してください[I/O 制御コードの説明をバッファー](buffer-descriptions-for-i-o-control-codes.md)します。

このメソッドは、ドライバーを保証して I/O 制御要求を生成したスレッドのコンテキストで実行されている場合にのみ使用できます。 最上位レベルのカーネル モード ドライバーのみをそのメソッドのこの条件を満たすことが保証\_低レベル デバイス ドライバーに渡される I/O コントロール コードのどちらもめったに使用します。

この方法で、最上位レベルのドライバーする必要がありますを決定するバッファーを設定するかどうかまたは可能性があります、要求の受信時にユーザー データへの直接アクセスは、ユーザー バッファーをロックダウンする必要があり、構造化例外ハンドラーでユーザー バッファーへのアクセスをラップする必要があります (を参照してください「。c1/>例外を処理する](handling-exceptions.md))。 それ以外の場合、元のユーザー モードの呼び出し元は、ドライバーが使用、またはドライバーがユーザー バッファーへのアクセスと同様、呼び出し元をスワップ アウトする可能性があります前に、バッファー内のデータを変更可能性があります。

詳細については、次を参照してください。[を使用していないバッファー Nor ダイレクト I/O](using-neither-buffered-nor-direct-i-o.md)します。

<a href="" id="requiredaccess"></a>*RequiredAccess*  
呼び出し元が要求する必要がありますアクセスの種類を示すデバイスを表すファイル オブジェクトを開くときに (を参照してください[ **IRP\_MJ\_作成**](https://msdn.microsoft.com/library/windows/hardware/ff550729))。 I/O マネージャー Irp が作成され、呼び出し元が指定したアクセス権を要求した場合にのみ使用してドライバーを特定の I/O 制御コードを呼び出します。 *RequiredAccess*は、次のシステム定義の定数を使用して指定します。

<a href="" id="file-any-access"></a>ファイル\_ANY\_アクセス  
I/O マネージャーでは、ターゲット デバイス オブジェクトを表すファイル オブジェクトへのハンドルを持つ呼び出し元の IRP が送信されます。

<a href="" id="file-read-data"></a>ファイル\_読み取り\_データ  
I/O マネージャーは、デバイスからシステム メモリにデータを転送する基になるデバイス ドライバーをできるように、読み取りアクセス権を持つ呼び出し元に対してのみ、IRP を送信します。

<a href="" id="file-write-data"></a>ファイル\_書き込み\_データ  
I/O マネージャーは、システム メモリからそのデバイスにデータを転送する基になるデバイス ドライバーを許可する、書き込みアクセス権を持つ呼び出し元に対してのみ、IRP を送信します。

ファイル\_読み取り\_データとファイル\_書き込み\_できるデータ//まとめて、呼び出し元には読み取りおよび書き込みアクセス権が必要がある場合。

システム定義の I/O 制御コードが、 *RequiredAccess*ファイルの値\_ANY\_呼び出し側が付与されるアクセス権に関係なく、特定の IOCTL をデバイスに送信するためのアクセス。 例としては、I/O 制御コードのドライバーに送信される*排他デバイス*します。

その他のシステム定義の I/O 制御コードには、呼び出し元に読み取りアクセス権や、書き込みアクセス権が必要です。 次のパブリックの I/O 制御コード IOCTL の定義など、\_ディスク\_設定\_パーティション\_この I/O 要求送信できることをドライバーに呼び出し元である場合にのみ読み取り/書き込みアクセス両方の情報が表示されます権限:

```cpp
#define IOCTL_DISK_SET_PARTITION_INFO\
        CTL_CODE(IOCTL_DISK_BASE, 0x008, METHOD_BUFFERED,\
        FILE_READ_DATA | FILE_WRITE_DATA)
```

**注**  ファイルを指定する前に\_ANY\_へのアクセスに新しい IOCTL コードを行うために、デバイスへの無制限のアクセス許可も悪意のあるユーザーの可能なパスは作成されませんが特定システムが侵害されます。

 

ドライバーを使用できる[ **IoValidateDeviceIoControlAccess** ](https://msdn.microsoft.com/library/windows/hardware/ff550418)より厳密なアクセスを実行する IOCTL のによって提供されるよりもチェック*RequiredAccess*ビット。

## <a name="other-useful-macros"></a>その他の便利なマクロ


次のマクロは、16 ビットを抽出するために役立ちます*DeviceType*と 2 ビット*TransferType* IOCTL コードからのフィールド。

```cpp
#define DEVICE_TYPE_FROM_CTL_CODE(ctrlCode)   (((ULONG)(ctrlCode & 0xffff0000)) >> 16)
#define METHOD_FROM_CTL_CODE(ctrlCode)        ((ULONG)(ctrlCode & 3))
```

これらのマクロは、Wdm.h と Ntddk.h で定義されます。

 

 




