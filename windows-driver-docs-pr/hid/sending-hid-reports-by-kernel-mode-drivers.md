---
title: カーネル モード ドライバーでの HID レポートを送信します。
description: カーネル モード ドライバーでの HID レポートを送信します。
ms.assetid: ff3d090f-cf76-40a7-9215-8440a592f303
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d19f85569a04c35f05a9937afdaf16737e5a849b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345453"
---
# <a name="sending-hid-reports-by-kernel-mode-drivers"></a>カーネル モード ドライバーでの HID レポートを送信します。


カーネル モード ドライバーを使用する必要があります[ **IRP\_MJ\_書き込み**](https://msdn.microsoft.com/library/windows/hardware/ff550819) HID コレクションにレポート出力を継続的に送信する要求の主なアプローチとして。 ドライバーは、IOCTL を使用できますも\_HID\_設定\_*Xxx*出力レポートを送信し、機能のコレクションにレポートを要求します。 ただし、ドライバーでは、コレクションの現在の状態を設定するのにこれらの I/O 要求が使用する必要がありますのみ。 一部のデバイスをサポートしていない[ **IOCTL\_HID\_設定\_出力\_レポート**](https://msdn.microsoft.com/library/windows/hardware/ff541196)され、この要求を使用する場合に応答しなくなります。

詳細については、次を参照してください。[を使用して IRP\_MJ\_書き込み要求](#using-irp-mj-write-requests)と[を使用して IOCTL\_HID\_設定\_Xxx 要求](#using-ioctl-hid-set-xxx-requests)します。

### <a href="" id="using-irp-mj-write-requests"></a>IRP を使用して\_MJ\_書き込み要求

Windows 2000 の非 WDM ドライバー、および Windows XP およびそれ以降のバージョンのドライバーは、コレクションに送信されたすべての書き込み要求の 1 つの IRP を使用できます。 ただし、Windows 2000 WDM ドライバーでは、書き込み要求ごとに新しい IRP を割り当てる必要があります。 使用して、Irp を再利用する方法の詳細については、次を参照してください。 [Irp の処理](https://msdn.microsoft.com/library/windows/hardware/ff546847)と[Irp の再利用](https://msdn.microsoft.com/library/windows/hardware/ff561107)します。

ドライバーを書き込み、IRP IRP の再利用かどうか[ **IoCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff548354)ルーチンは、状態の状態で要求を完了する必要があります\_詳細\_処理\_REQUIRED (および IRP を解放)。 ドライバーは IRP が不要になった必要がある場合、完了して IRP を呼び出すことによって解放[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)と[ **IoFreeIrp**](https://msdn.microsoft.com/library/windows/hardware/ff549113)します。 たとえば、ドライバー可能性があります通常完了し、解放で IRP その[**アンロード**](https://msdn.microsoft.com/library/windows/hardware/ff564886)ルーチン、以降のデバイスを削除します。

1 つだけの書き込み要求は、IRP のドライバーが IRP を使用する場合[ **IoCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff548354)完了し、IRP を無料し、状態を返す必要がありますルーチン\_成功します。

出力レポートを送信する前に、ドライバー、まず初期化しで説明したように、出力レポート バッファーを設定[HID レポートの初期化](initializing-hid-reports.md)します。 ドライバーは、書き込み要求の出力バッファーにレポートにマップするのに、MDL を使用する必要があります。 ドライバーを呼び出す[ **IoAllocateMdl** ](https://msdn.microsoft.com/library/windows/hardware/ff548263) MDL の出力レポート、および書き込み IRP をセットの割り当てを**Irp -&gt;MdlAddress**メンバーの MDL アドレスに、レポートの出力バッファー。 ドライバーは、必要でなくなったときに、レポート バッファーと MDL を解放する必要があります。

書き込みの IRP MDL アドレスを設定するには、に加えて、ドライバーは、[次へ] の下位レベルのドライバーの I/O スタックの場所にも設定する必要があります。 ドライバーを呼び出すことによって、[次へ] の下位レベルのドライバーの I/O スタックの場所へのアクセスを取得する[ **IoGetNextIrpStackLocation**](https://msdn.microsoft.com/library/windows/hardware/ff549266)します。 ドライバーは、I/O スタックの場所の次のメンバーを設定します。

<a href="" id="parameters-write-length"></a>**Parameters.Write.Length**  
レポートの出力の長さ、(バイト単位) を設定します。 これは、HID コレクションの出力レポートで指定したとおりの長さに設定する必要があります、 **OutputReportByteLength**コレクションのメンバー [ **HIDP\_CAP** ](https://msdn.microsoft.com/library/windows/hardware/ff539697)構造体。

<a href="" id="parameters-write-key"></a>**Parameters.Write.Key**  
0 に設定します。

<a href="" id="parameters-write-byteoffset-quadpart"></a>**Parameters.Write.ByteOffset.QuadPart**  
0 に設定します。

<a href="" id="majorfunction"></a>**MajorFunction**  
IRP に設定\_MJ\_を記述します。

<a href="" id="fileobject"></a>**FileObject**  
HID コレクションで、開いているファイルを表すファイル オブジェクト ポインターに設定します。

### <a href="" id="using-ioctl-hid-set-xxx-requests"></a>IOCTL を使用して\_HID\_設定\_Xxx 要求

ドライバーはことができますも、次の I/O 要求を使用して出力を送信して、HID コレクションにレポートを機能。

<a href="" id="ioctl-hid-set-output-report"></a>[**IOCTL\_HID\_設定\_出力\_レポート**](https://msdn.microsoft.com/library/windows/hardware/ff541196)  
(Windows XP およびそれ以降のバージョン) のコレクションを出力レポートを送信します。

<a href="" id="ioctl-hid-set-feature"></a>[**IOCTL\_HID\_設定\_機能**](https://msdn.microsoft.com/library/windows/hardware/ff541176)  
コレクションには、機能のレポートを送信します。

 

 




