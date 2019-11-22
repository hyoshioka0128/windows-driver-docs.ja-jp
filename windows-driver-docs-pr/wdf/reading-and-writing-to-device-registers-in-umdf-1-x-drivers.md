---
title: UMDF 1.x ドライバーでのデバイス レジスターの読み取りと書き込み
description: UMDF 1.x ドライバーでのデバイス レジスターの読み取りと書き込み
ms.assetid: A0640E60-B0DF-4CAD-B292-CC1875EF7F7D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2070778a2e61c2065ace8c129abcb54fd2a495ad
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842228"
---
# <a name="reading-and-writing-to-device-registers-in-umdf-1x-drivers"></a>UMDF 1.x ドライバーでのデバイス レジスターの読み取りと書き込み


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

UMDF バージョン1.11 以降、フレームワークには、メモリ領域と i/o ポート領域のレジスタにアクセスするためのルーチンのセットが用意されています。 [UMDF register/port アクセスルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/)は、カーネルモードドライバーによって使用される HAL ルーチンとよく似ています。 「 [UMDF ドライバーでのハードウェアリソースの検索とマッピング](https://docs.microsoft.com/windows-hardware/drivers/wdf/finding-and-mapping-hardware-resources-in-umdf-1-x-drivers)」で説明されているように、ドライバーによってレジスタがマップされた後、ドライバーは読み取り/書き込み\_REGISTER\_Xxx ルーチンを使用して個々のレジスタの読み取りと書き込みを行います。 I/o ポートの場合、ドライバーは読み取り/書き込み\_ポート\_Xxx ルーチンを呼び出します。

この例では、メモリマップトレジスタに書き込む方法を示します。

```cpp
VOID
CMyQueue::WriteToDevice(
    __in IWDFDevice3* pWdfDevice,
    __in UCHAR Value
    )
{
    //
    // Write the UCHAR value at offset 2 from register base
    //
    WRITE_REGISTER_UCHAR(pWdfDevice, 
                      (m_MyDevice->m_RegBase)+2, 
                       Value);
}
```

既定では、UMDF は、内部的にシステム呼び出しを使用して、メモリ領域または i/o ポート領域にマップされているレジスタにアクセスします。 I/o ポート領域への登録には、常にシステムコールを使用してアクセスします。 ただし、メモリマップトレジスタにアクセスする場合、UMDF driver は、INF ディレクティブ**Umdfregisteraccessmode**を**RegisterAccessUsingUserModeMapping**に設定することによって、フレームワークがメモリマップトレジスタをユーザーモードアドレス空間にマップすることがあります。 一部のドライバーでは、パフォーマンス上の理由により、この操作が必要になる場合があります。 UMDF INF ディレクティブの完全な一覧については、「 [WDF ディレクティブを INF ファイルに指定する](specifying-wdf-directives-in-inf-files.md)」を参照してください。

ドライバーは、レジスタがユーザーモードにマップされている場合でも、読み取り/書き込み\_を\_Xxx ルーチンに登録する必要があります。 これらのルーチンは、ドライバーの入力を検証し、ドライバーが無効な場所へのアクセスを要求しないようにします。 ほとんどの場合、ドライバーは、これらのルーチンを使用せずに、ユーザーモードでマップされたレジスタに直接アクセスする必要があります。 これを行うには、マップされたベースアドレスで[**IWDFDevice3:: GetHardwareRegisterMappedAddress**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice3-gethardwareregistermappedaddress)を呼び出すことによって、ドライバーがユーザーモードでマップされたアドレスを取得します。 UMDF では、この方法で実行される読み取りアクセスと書き込みアクセスは検証されないため、登録アクセスにはこの手法を使用しないことをお勧めします。

 

 





