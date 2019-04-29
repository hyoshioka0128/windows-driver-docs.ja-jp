---
title: Winsock カーネル アプリケーションの登録解除
description: Winsock カーネル アプリケーションの登録解除
ms.assetid: f5d99c10-eeac-499e-8630-6aa188d38d75
keywords:
- Winsock カーネル WDK ネットワーク、登録します。
- Winsock カーネル アプリケーションの登録を解除
- WSK WDK ネットワーク、登録します。
- WskDeregister
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25d64c54369f74b2227c0b796475ba8a99ecedc5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324333"
---
# <a name="unregistering-a-winsock-kernel-application"></a>Winsock カーネル アプリケーションの登録解除


持つ WSK クライアントとして正常に登録されている、Winsock カーネル (WSK) アプリケーション、 [ **WskRegister** ](https://msdn.microsoft.com/library/windows/hardware/ff571143)関数を確認する必要がありますを[ **WskDeregister**](https://msdn.microsoft.com/library/windows/hardware/ff571128)が呼び出されたとドライバーの前に、呼び出しが返された[**アンロード**](https://msdn.microsoft.com/library/windows/hardware/ff564886)関数が返される。 呼ばれる WSK アプリケーション**WskRegister**正常に呼び出さずにアンロードしない**WskDeregister**、すべてのインスタンスを取得するまで、WSK クライアント オブジェクトの登録を解除する待機が、WSK プロバイダー NPI がと共にリリースされた[ **WskReleaseProviderNPI** ](https://msdn.microsoft.com/library/windows/hardware/ff571145)のすべてのソケットが WSK アプリケーションで閉じられているとします。 保留中の関数に渡された Irp がある場合[ **WSK\_プロバイダー\_ディスパッチ**](https://msdn.microsoft.com/library/windows/hardware/ff571175)、 **WskDeregister**もになるまで待機保留中の Irp を完了します。 WSK アプリケーション WSK で関数を呼び出す必要がありますしない\_プロバイダー\_後ディスパッチ**WskReleaseProviderNPI**が呼び出されます。

次に、例を示します。

```C++
// Unload function
VOID
  Unload(
    IN PDRIVER_OBJECT DriverObject
    )
{
  // Unregister the WSK application
  WskDeregister(
    &WskRegistration
    );

}
```

WSK アプリケーションは、必ずしも常に呼び出すには必要ありません**WskDeregister**内からその*アンロード*関数。 たとえば、WSK アプリケーションが複雑なドライバー、WSK アプリケーションの呼び出しのサブコンポーネント**WskDeregister** WSK アプリケーションのサブコンポーネントが非アクティブ化されたときに発生する可能性があります。 このようなシナリオで、ドライバーから返される前にその*アンロード*関数の場合、その必要がありますもことを確認 WSK アプリケーションが呼び出しを正常に登録されている**WskDeregister**します。

 

 





