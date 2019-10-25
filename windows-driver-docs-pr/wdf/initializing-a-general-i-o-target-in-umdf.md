---
title: UMDF での一般 I/O ターゲットの初期化
description: UMDF での一般 I/O ターゲットの初期化
ms.assetid: cf1b39c3-4c82-411b-8eef-117ac0fe793e
keywords:
- 一般的な i/o ターゲット WDK UMDF、初期化
- 一般的な i/o ターゲットの初期化 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9ae8b9fe69f008eeb9ad4de20793d1b0bfee238
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845445"
---
# <a name="initializing-a-general-io-target-in-umdf"></a>UMDF での一般 I/O ターゲットの初期化


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

一般的な i/o ターゲットを初期化するためにドライバーが使用する手順は、i/o ターゲットが[ローカル](general-i-o-targets-in-umdf.md)かリモートかによって異なります。

### <a name="initializing-a-local-io-target"></a>ローカル i/o ターゲットの初期化

ローカル i/o ターゲットには、デバイスの[既定の i/o ターゲット](general-i-o-targets-in-umdf.md)とファイルハンドルベースの i/o ターゲットが含まれます。

このフレームワークは、ドライバーが[**Iwdfdriver:: CreateDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdriver-createdevice)メソッドを呼び出すと、デバイスの既定の i/o ターゲットを初期化します。 ドライバーがデバイスの既定の i/o ターゲットにアクセスできるようにする[Iwdfiotarget](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiotarget)インターフェイスを取得するために、ドライバーは[**Iwdfdevice:: GetDefaultIoTarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-getdefaultiotarget)メソッドを呼び出します。

ほとんどのドライバーは、既定の i/o ターゲットにのみ要求を送信します。

UMDF ドライバーがネットワークソケットインターフェイスなどのハンドルベースのインターフェイスに i/o 要求を送信する必要がある場合、ドライバーはファイルハンドルベースの i/o ターゲットオブジェクトを作成する必要があります。 ファイルハンドルベースの i/o ターゲットオブジェクトを作成するには、ドライバーは次の操作を行う必要があります。

1.  デバイスの[Iwdfdevice](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdevice)インターフェイスの**QueryInterface**メソッドを呼び出して、 [Iwdffilehandletargetfactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdffilehandletargetfactory)インターフェイスへのポインターを取得します。

2.  Win32 [**CreateFile**](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-createfilea)、 **CreateNamedPipe**、または**socket**関数を呼び出して、ファイル、名前付きパイプ、またはソケットへの win32 ハンドルを取得します。

3.  [**Iwdffilehandletargetfactory:: createfilehandletarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdffilehandletargetfactory-createfilehandletarget)メソッドを呼び出して、ファイルハンドルベースの i/o ターゲットオブジェクトをファイル、パイプ、またはソケットに作成します。

[Iwdffilehandletargetfactory](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdffilehandletargetfactory)インターフェイスを取得し、Win32 ハンドルを取得し、ファイルハンドルベースの i/o ターゲットオブジェクトを作成する方法を示すコード例については、 [**Iwdffilehandletargetfactory:: CreateFileHandleTarget にあるコード例を参照してください。** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdffilehandletargetfactory-createfilehandletarget).

ドライバーがファイルハンドルベースの i/o ターゲットを作成した後、ドライバーは i/o ターゲットに i/o 要求を送信できます。

### <a name="initializing-a-remote-io-target"></a>リモート i/o ターゲットの初期化

ドライバーがリモート i/o ターゲットを使用できるようにするには、次のように、リモートターゲットオブジェクトを作成し、ターゲットを開く必要があります。

1.  [**IWDFDevice2:: CreateRemoteTarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice2-createremotetarget)を呼び出して、リモートのターゲットオブジェクトを作成します。

2.  [**Iwdfremotetarget:: OpenFileByName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-openfilebyname) (ファイルの場合) または[**Iwdfremotetarget:: openremoteinterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-openremoteinterface) ([デバイスインターフェイス](using-device-interfaces-in-umdf-drivers.md)の場合) のいずれかを呼び出して、i/o 操作のターゲットを開きます。

 

 





