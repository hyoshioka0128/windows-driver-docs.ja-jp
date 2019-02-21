---
title: UMDF で一般的な I/O ターゲットの初期化
description: UMDF で一般的な I/O ターゲットの初期化
ms.assetid: cf1b39c3-4c82-411b-8eef-117ac0fe793e
keywords:
- 一般的な I/O WDK UMDF、初期化の対象します。
- WDK UMDF を対象と一般的な I/O の初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85099a67f1f3fb14c468b184f9fcebf248236777
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56553853"
---
# <a name="initializing-a-general-io-target-in-umdf"></a>UMDF で一般的な I/O ターゲットの初期化


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

一般的な I/O ターゲットを初期化するために、ドライバーを使用する手順は、I/O のターゲットがかどうかによって異なります[ローカル](general-i-o-targets-in-umdf.md)またはリモートです。

### <a name="initializing-a-local-io-target"></a>ローカルの I/O ターゲットの初期化

ローカルの I/O ターゲットには、デバイスの[I/O の既定のターゲット](general-i-o-targets-in-umdf.md)および I/O のターゲットのファイル ハンドル ベースです。

ドライバーを呼び出すと、フレームワークに、デバイスのドライバーの既定の I/O ターゲットを初期化します、 [ **IWDFDriver::CreateDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff558899)メソッド。 取得する、 [IWDFIoTarget](https://msdn.microsoft.com/library/windows/hardware/ff559170) 、ドライバー、デバイスの既定の I/O ターゲット、ドライバーの呼び出しにアクセスできるようにするインターフェイス、 [ **IWDFDevice::GetDefaultIoTarget** ](https://msdn.microsoft.com/library/windows/hardware/ff558831)メソッド。

ほとんどのドライバーでは、その既定の I/O ターゲットにのみ要求を送信します。

UMDF ドライバーは、ネットワーク ソケット インターフェイスなどのハンドルに基づくインターフェイスの I/O 要求を送信する必要がある場合、ドライバーは、ファイル ハンドル ベースの I/O ターゲット オブジェクトを作成する必要があります。 ファイル ハンドル ベースの I/O ターゲット オブジェクトを作成するには、ドライバーは、次の操作を行う必要があります。

1.  呼び出す、 **QueryInterface**メソッド、デバイスの[IWDFDevice](https://msdn.microsoft.com/library/windows/hardware/ff556917)へのポインターを取得するインターフェイス、 [IWDFFileHandleTargetFactory](https://msdn.microsoft.com/library/windows/hardware/ff558926)インターフェイス。

2.  Win32 を呼び出すことによって、ファイル、名前付きパイプ、またはソケットに Win32 ハンドルを取得[ **CreateFile**](https://msdn.microsoft.com/library/windows/desktop/aa363858)、 **CreateNamedPipe**、または**ソケット**関数.

3.  呼び出す、 [ **IWDFFileHandleTargetFactory::CreateFileHandleTarget** ](https://msdn.microsoft.com/library/windows/hardware/ff558930)ファイル、パイプ、またはソケットのファイル ハンドル ベースの I/O ターゲット オブジェクトを作成します。

取得する方法を示すコード例については、 [IWDFFileHandleTargetFactory](https://msdn.microsoft.com/library/windows/hardware/ff558926)インターフェイス、Win32 ハンドルを取得し、ファイル ハンドル ベースの I/O ターゲット オブジェクトを作成、コード例を参照[ **IWDFFileHandleTargetFactory::CreateFileHandleTarget**](https://msdn.microsoft.com/library/windows/hardware/ff558930)します。

ドライバーがファイル ハンドル ベースの I/O ターゲットを作成した後、ドライバーは、I/O ターゲットを I/O 要求を送信できます。

### <a name="initializing-a-remote-io-target"></a>リモートの I/O ターゲットの初期化

ドライバーは、リモートの I/O ターゲットを使用して、前に、リモート ターゲット オブジェクトを作成し、次のように、ターゲットを開きますする必要があります。

1.  呼び出す[ **IWDFDevice2::CreateRemoteTarget** ](https://msdn.microsoft.com/library/windows/hardware/ff556928)リモート ターゲット オブジェクトを作成します。

2.  いずれかを呼び出す[ **IWDFRemoteTarget::OpenFileByName** ](https://msdn.microsoft.com/library/windows/hardware/ff560273) (ファイル用) または[ **IWDFRemoteTarget::OpenRemoteInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff560276) (用[デバイス インターフェイス](using-device-interfaces-in-umdf-drivers.md)) I/O 操作のターゲットを開きます。

 

 





