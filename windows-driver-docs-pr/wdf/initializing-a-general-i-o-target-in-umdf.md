---
title: UMDF での一般 I/O ターゲットの初期化
description: UMDF での一般 I/O ターゲットの初期化
ms.assetid: cf1b39c3-4c82-411b-8eef-117ac0fe793e
keywords:
- 一般的な I/O WDK UMDF、初期化の対象します。
- WDK UMDF を対象と一般的な I/O の初期化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2cfd2f92d81ff34e31b4cd427847cc032db9198
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380579"
---
# <a name="initializing-a-general-io-target-in-umdf"></a>UMDF での一般 I/O ターゲットの初期化


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

一般的な I/O ターゲットを初期化するために、ドライバーを使用する手順は、I/O のターゲットがかどうかによって異なります[ローカル](general-i-o-targets-in-umdf.md)またはリモートです。

### <a name="initializing-a-local-io-target"></a>ローカルの I/O ターゲットの初期化

ローカルの I/O ターゲットには、デバイスの[I/O の既定のターゲット](general-i-o-targets-in-umdf.md)および I/O のターゲットのファイル ハンドル ベースです。

ドライバーを呼び出すと、フレームワークに、デバイスのドライバーの既定の I/O ターゲットを初期化します、 [ **IWDFDriver::CreateDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdriver-createdevice)メソッド。 取得する、 [IWDFIoTarget](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfiotarget) 、ドライバー、デバイスの既定の I/O ターゲット、ドライバーの呼び出しにアクセスできるようにするインターフェイス、 [ **IWDFDevice::GetDefaultIoTarget** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-getdefaultiotarget)メソッド。

ほとんどのドライバーでは、その既定の I/O ターゲットにのみ要求を送信します。

UMDF ドライバーは、ネットワーク ソケット インターフェイスなどのハンドルに基づくインターフェイスの I/O 要求を送信する必要がある場合、ドライバーは、ファイル ハンドル ベースの I/O ターゲット オブジェクトを作成する必要があります。 ファイル ハンドル ベースの I/O ターゲット オブジェクトを作成するには、ドライバーは、次の操作を行う必要があります。

1.  呼び出す、 **QueryInterface**メソッド、デバイスの[IWDFDevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdevice)へのポインターを取得するインターフェイス、 [IWDFFileHandleTargetFactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdffilehandletargetfactory)インターフェイス。

2.  Win32 を呼び出すことによって、ファイル、名前付きパイプ、またはソケットに Win32 ハンドルを取得[ **CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)、 **CreateNamedPipe**、または**ソケット**関数.

3.  呼び出す、 [ **IWDFFileHandleTargetFactory::CreateFileHandleTarget** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdffilehandletargetfactory-createfilehandletarget)ファイル、パイプ、またはソケットのファイル ハンドル ベースの I/O ターゲット オブジェクトを作成します。

取得する方法を示すコード例については、 [IWDFFileHandleTargetFactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdffilehandletargetfactory)インターフェイス、Win32 ハンドルを取得し、ファイル ハンドル ベースの I/O ターゲット オブジェクトを作成、コード例を参照[ **IWDFFileHandleTargetFactory::CreateFileHandleTarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdffilehandletargetfactory-createfilehandletarget)します。

ドライバーがファイル ハンドル ベースの I/O ターゲットを作成した後、ドライバーは、I/O ターゲットを I/O 要求を送信できます。

### <a name="initializing-a-remote-io-target"></a>リモートの I/O ターゲットの初期化

ドライバーは、リモートの I/O ターゲットを使用して、前に、リモート ターゲット オブジェクトを作成し、次のように、ターゲットを開きますする必要があります。

1.  呼び出す[ **IWDFDevice2::CreateRemoteTarget** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice2-createremotetarget)リモート ターゲット オブジェクトを作成します。

2.  いずれかを呼び出す[ **IWDFRemoteTarget::OpenFileByName** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfremotetarget-openfilebyname) (ファイル用) または[ **IWDFRemoteTarget::OpenRemoteInterface** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfremotetarget-openremoteinterface) (用[デバイス インターフェイス](using-device-interfaces-in-umdf-drivers.md)) I/O 操作のターゲットを開きます。

 

 





