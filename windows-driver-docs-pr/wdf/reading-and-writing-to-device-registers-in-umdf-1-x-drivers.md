---
title: UMDF 1.x ドライバーでのデバイス レジスターの読み取りと書き込み
description: UMDF 1.x ドライバーでのデバイス レジスターの読み取りと書き込み
ms.assetid: A0640E60-B0DF-4CAD-B292-CC1875EF7F7D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fccf6f0d5b01bc470479d6145c30b019584772c1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376309"
---
# <a name="reading-and-writing-to-device-registers-in-umdf-1x-drivers"></a>UMDF 1.x ドライバーでのデバイス レジスターの読み取りと書き込み


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

フレームワークは UMDF バージョン 1.11 以降、メモリの容量と I/O ポートの領域でのレジスタにアクセスするルーチンのセットを提供します。 [UMDF 登録/ポート アクセス ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/)カーネル モード ドライバーで使用される HAL ルーチンとよく似ています。 」の説明に従って、ドライバーのレジスタがマップする後[UMDF ドライバーでのハードウェア リソースのマッピングの検索と](https://docs.microsoft.com/windows-hardware/drivers/wdf/finding-and-mapping-hardware-resources-in-umdf-1-x-drivers)、ドライバーは、読み取り/書き込みを使用\_登録\_読み取りし、書き込みを個別に Xxx ルーチン登録します。 I/O ポート、ドライバーの呼び出し、読み取り/書き込み\_ポート\_Xxx ルーチン。

この例では、メモリ マップト レジスタに書き込む方法を示します。

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

既定では、UMDF は内部的にメモリ領域で、または I/O ポートの領域にマップされているレジスタにアクセスするのにシステム コールを使用します。 I/O ポートの領域でのレジスタは常にシステム呼び出しを通じてアクセスします。 ただし、メモリ マップト レジスタへのアクセスを UMDF ドライバーが原因 INF ディレクティブを設定してユーザー モード アドレス空間にメモリ マップト レジスタにマップするためにフレームワーク**UmdfRegisterAccessMode**に**RegisterAccessUsingUserModeMapping**します。 一部のドライバーは、このパフォーマンス上の理由に対して行う必要があります。 参照してください[INF ファイルで WDF ディレクティブを指定する](specifying-wdf-directives-in-inf-files.md)UMDF INF ディレクティブの完全な一覧についてはします。

ドライバーは、読み取り/書き込みを使用する必要があります\_登録\_Xxx ルーチンがユーザー モードにレジスタがマップされた場合でもです。 これらのルーチンでは、ドライバーの入力を検証し、ドライバーが無効な場所へのアクセスを要求しないことを確認します。 まれには、ドライバーは、ユーザー モードでマップされているレジスタを直接、これらのルーチンを使用せずにアクセスする必要があります。 ドライバーは、ユーザー モードを取得します。 そのためには、呼び出すことでアドレスをマップ[ **IWDFDevice3::GetHardwareRegisterMappedAddress** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice3-gethardwareregistermappedaddress)にマップされたベース アドレス。 UMDF は読み取りを検証し、この方法で実行するアクセスの書き込みありません、ため、この手法はレジスタへのアクセスは推奨されません。

 

 





