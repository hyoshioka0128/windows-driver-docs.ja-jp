---
title: 読み取りと書き込みをデバイスには、UMDF 1.x ドライバーで登録します
description: 読み取りと書き込みをデバイスには、UMDF 1.x ドライバーで登録します
ms.assetid: A0640E60-B0DF-4CAD-B292-CC1875EF7F7D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 189fa29ee87fa0214b34a6201b27dcf13e7e906b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556912"
---
# <a name="reading-and-writing-to-device-registers-in-umdf-1x-drivers"></a>読み取りと書き込みをデバイスには、UMDF 1.x ドライバーで登録します


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

フレームワークは UMDF バージョン 1.11 以降、メモリの容量と I/O ポートの領域でのレジスタにアクセスするルーチンのセットを提供します。 [UMDF 登録/ポート アクセス ルーチン](https://msdn.microsoft.com/library/windows/hardware/hh463975)カーネル モード ドライバーで使用される HAL ルーチンとよく似ています。 」の説明に従って、ドライバーのレジスタがマップする後[UMDF ドライバーでのハードウェア リソースのマッピングの検索と](https://msdn.microsoft.com/library/windows/hardware/hh439594)、ドライバーは、読み取り/書き込みを使用\_登録\_読み取りし、書き込みを個別に Xxx ルーチン登録します。 I/O ポート、ドライバーの呼び出し、読み取り/書き込み\_ポート\_Xxx ルーチン。

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

ドライバーは、読み取り/書き込みを使用する必要があります\_登録\_Xxx ルーチンがユーザー モードにレジスタがマップされた場合でもです。 これらのルーチンでは、ドライバーの入力を検証し、ドライバーが無効な場所へのアクセスを要求しないことを確認します。 まれには、ドライバーは、ユーザー モードでマップされているレジスタを直接、これらのルーチンを使用せずにアクセスする必要があります。 ドライバーは、ユーザー モードを取得します。 そのためには、呼び出すことでアドレスをマップ[ **IWDFDevice3::GetHardwareRegisterMappedAddress** ](https://msdn.microsoft.com/library/windows/hardware/hh451219)にマップされたベース アドレス。 UMDF は読み取りを検証し、この方法で実行するアクセスの書き込みありません、ため、この手法はレジスタへのアクセスは推奨されません。

 

 





