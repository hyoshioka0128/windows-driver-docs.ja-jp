---
title: I/O 制御コードのバッファー記述
description: I/O 制御コードのバッファー記述
ms.assetid: a458f3fb-a6c7-42ae-870e-1617a96b496f
keywords:
- I/O 制御コード WDK カーネル、バッファーの説明
- 制御コード WDK Ioctl、バッファーの説明
- Ioctl WDK カーネルでは、バッファーの説明
- バッファーの WDK Ioctl の説明
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8af2d869f1f3760affb5afcc083e30cf48549d5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326044"
---
# <a name="buffer-descriptions-for-io-control-codes"></a>I/O 制御コードのバッファー記述





I/O 制御コードに含まれる[ **IRP\_MJ\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550744)と[ **IRP\_MJ\_内部\_デバイス\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550766)要求。 I/O マネージャーは、呼び出しの結果としてこれらの要求を作成します[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216) (Microsoft Windows SDK のドキュメントで説明) と[  **。IoBuildDeviceIoControlRequest**](https://msdn.microsoft.com/library/windows/hardware/ff548318)します。

[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)と**IoBuildDeviceIoControlRequest**入力バッファーと出力バッファーの両方を引数として受け入れるすべて**IRP\_MJ\_デバイス\_コントロール**と**IRP\_MJ\_内部\_デバイス\_コントロール**要求は、両方の入力を指定バッファーと出力バッファー。 システムは、これらのバッファーを説明します。 方法は、データ転送の種類に依存です。 転送の種類がで指定された、 *TransferType*値、 [ **CTL\_コード**](defining-i-o-control-codes.md)マクロ IOCTL コード値を作成します。

システムは、各バッファーをについて説明します*TransferType*値を次のようにします。

<a href="" id="method-buffered"></a>メソッド\_バッファーに格納されました。  
この転送の種類の Irp が、バッファーへのポインターを指定**Irp -&gt;AssociatedIrp.SystemBuffer**します。 このバッファーは、入力バッファーと出力バッファーへの呼び出しで指定されているの両方を表す[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)と**IoBuildDeviceIoControlRequest**します。 ドライバーでは、サインアウトし、このバッファーにデータを転送します。

入力データのバッファー サイズが指定された**Parameters.DeviceIoControl.InputBufferLength**ドライバーの[ **IO\_スタック\_場所**](https://msdn.microsoft.com/library/windows/hardware/ff550659)構造体。 出力データ バッファーのサイズが指定された**Parameters.DeviceIoControl.OutputBufferLength**ドライバーの**IO\_スタック\_場所**構造体。

1 つの入力/出力バッファーが 2 つの長さの値のうち、大きい方には、システムによって割り当てられる領域のサイズ。

<a href="" id="method-in-direct-or-method-out-direct"></a>メソッド\_IN\_ダイレクトまたはメソッド\_アウト\_ダイレクト  
これらの種類の転送の Irp がでバッファーへのポインターを指定**Irp -&gt;AssociatedIrp.SystemBuffer**します。 これはへの呼び出しで指定されている入力のバッファーを表します**DeviceIoControl**と**IoBuildDeviceIoControlRequest**します。 バッファー サイズがで指定された**Parameters.DeviceIoControl.InputBufferLength**ドライバーの**IO\_スタック\_場所**構造体。

これらの種類の転送の Irp 指定することも、MDL でへのポインター **Irp -&gt;MdlAddress**します。 これはへの呼び出しで指定されている出力バッファーを表します[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)と**IoBuildDeviceIoControlRequest**します。 ただし、このバッファーは実際にように使用、入力バッファーまたは出力バッファーとして。

-   メソッド\_IN\_が呼び出されると、IRP を処理するドライバーがバッファーにデータを受け取るかどうか DIRECT を指定します。 MDL は、入力バッファーとメソッドの指定について説明します。\_IN\_ダイレクトは、実行中のスレッドが、バッファーへの読み取りアクセスをあることを確認します。

-   メソッド\_アウト\_IRP を処理するドライバーが IRP を完了する前に、バッファーにデータを書き込むはかどうか DIRECT を指定します。 MDL は、出力バッファー、およびメソッドの指定について説明します。\_アウト\_ダイレクトは、実行中のスレッドが、バッファーへの書き込みアクセスをあることを確認します。

これらの種類の転送の両方の**Parameters.DeviceIoControl.OutputBufferLength** MDL によって記述されるバッファーのサイズを指定します。

<a href="" id="method-neither"></a>メソッド\_NEITHER  
I/O マネージャーでは、任意のシステムのバッファーまたは MDLs は提供されません。 IRP が提供するために指定された入力と出力バッファーのユーザー モード仮想アドレス**DeviceIoControl**または**IoBuildDeviceIoControlRequest**の検証またはマッピングすることなしに、します。

によって、入力バッファーのアドレスが提供される**Parameters.DeviceIoControl.Type3InputBuffer**ドライバーの**IO\_スタック\_場所**構造、および、出力バッファーのアドレスがで指定された**Irp -&gt;UserBuffer**します。

バッファー サイズがによって提供される**Parameters.DeviceIoControl.InputBufferLength**と**Parameters.DeviceIoControl.OutputBufferLength**ドライバーの**IO\_スタック\_場所**構造体。

詳細については、 **CTL\_コード**マクロと転送の種類を上記を参照してください。 [I/O 制御コードを定義する](defining-i-o-control-codes.md)します。

 

 




