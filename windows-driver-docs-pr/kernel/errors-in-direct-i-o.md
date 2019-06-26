---
title: ダイレクト I/O のエラー
description: ダイレクト I/O のエラー
ms.assetid: 9efc2875-3402-4e2e-871b-3cc1d8f45360
keywords:
- 信頼性 WDK カーネルでは、ダイレクト I/O
- ダイレクト I/O WDK カーネル
- I/O WDK カーネルでは、ダイレクト I/O
- バッファーの長さ 0 の WDK カーネル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84ed8c1e26df36f609ddabb8d1b2e94853ba31ab
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385125"
---
# <a name="errors-in-direct-io"></a>ダイレクト I/O のエラー





ダイレクト I/O の最も一般的な問題は、長さ 0 のバッファーを正しく処理するために失敗しています。 長さ 0 のバッファーの結果が I/O マネージャーが長さ 0 の転送 MDLs を作成しないためです、 **NULL**値**Irp -&gt;MdlAddress**。

アドレス空間をマップするドライバーを使用する必要があります[ **MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)、返された**NULL**をドライバーに渡すかどうか、失敗した場合をマッピングする場合は、 **NULL** **MdlAddress**します。 ドライバーを常に確認する必要があります、 **NULL**返されたアドレスを使用する前に戻り値。

Double 型のマッピングは、システム アドレス バッファーに、ユーザーのアドレス空間をダイレクト I/O、2 つの異なる仮想アドレスが同じ物理アドレスを持つようにします。 Double 型のマッピングには、次の結果は、ドライバーの問題が生じる場合がありますがあります。

-   仮想ユーザーのアドレスのページへのオフセットでは、システムのページに、オフセットになります。

    これらのシステムのバッファーの末尾の次のアクセスをマッピングのページの粒度によっては時間が長い可能性があります気付かれない。 ページの末尾付近の呼び出し元のバッファーが割り当てられると、しない限り、バッファー、バッファーの末尾を越える書き込まれたデータが表示されますそれでもと、呼び出し元は、エラーが発生したことが認識されません。 ページの末尾と一致するバッファーの末尾、末尾の次のシステムの仮想アドレスはものを指すことができますか、有効でない可能性があります。 このような問題を検索する非常に困難になります。

-   呼び出し元のプロセスにメモリのユーザーのマッピングを変更する別のスレッドがある場合は、システムのバッファーの内容は、ユーザーのメモリ マッピングが変更されたときに変更されます。

    このような状況では、スクラッチ データを格納するシステムのバッファーを使用すると、問題が発生することができます。 同じメモリ位置からの 2 つのフェッチでは、別の値を生成可能性があります。

    次のコード スニペットでは、ダイレクト I/O 要求では文字列を受信し、その文字列を大文字に変換しようとしています。

    ```cpp
    PWCHAR  PortName = NULL;

    PortName = (PWCHAR)MmGetSystemAddressForMdlSafe(irp->MdlAddress, NormalPagePriority);

    //
    // Null-terminate the PortName so that RtlInitUnicodeString will not
    // be invalid.
    //
    PortName[Size / sizeof(WCHAR) - 1] = UNICODE_NULL;

    RtlInitUnicodeString(&AdapterName, PortName);
    ```

    コードが、Unicode を強制しようとしたバッファーが正しい形式でない可能性があります、ため**NULL**バッファーの最後の文字として。 ただし、基になる物理メモリがユーザーとカーネル モード アドレスの両方にマップされている二重場合、この書き込み操作が完了するとすぐに、別のスレッド、プロセスでは、バッファー上書きできます。

    逆に場合、 **NULL**が現在のところ、その呼び出し**RtlInitUnicodeString**バッファーの範囲を超えるし、システムのマッピングの外になる場合は、バグ チェックが原因として考えられることができます。

ドライバーは、作成し、独自の MDL のマップする場合、プローブされますが、メソッドでのみ、MDL にアクセスすることを確認する必要があります。 つまり、ドライバーを呼び出すと[ **MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmprobeandlockpages)、アクセス方法を指定します (**IoReadAccess**、 **IoWriteAccess**、または**IoModifyAccess**)。 ドライバーが指定されている場合**IoReadAccess**、によって提供されるシステムのバッファーに書き込む後で試行する必要がありますいない[ **MmGetSystemAddressForMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmgetsystemaddressformdl)または[**MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)します。

 

 




