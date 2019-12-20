---
title: ドライバー作成ファイル オブジェクトの作成と使用
description: ドライバー作成ファイル オブジェクトの作成と使用
ms.assetid: 84b677b4-fddf-4f06-9ea6-e4642c3f1b2d
keywords:
- ドライバーで作成されたファイルオブジェクト WDK UMDF
- ドライバーによって作成されたファイルオブジェクト WDK UMDF、作成と使用
- i/o WDK UMDF、ドライバー作成、作成、および使用を処理するファイルオブジェクト
- I/o 要求 WDK UMDF、ファイルオブジェクト、作成と使用
- ユーザーモードドライバーフレームワーク WDK、i/o を処理するためのファイルオブジェクト、作成および使用
- UMDF WDK、i/o を処理するためのファイルオブジェクト、作成と使用
- ユーザーモードドライバー WDK UMDF、i/o を処理するためのファイルオブジェクト、作成、使用
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5f2534fe60a6ce7d9137986a8e4ee1c2733d0e4
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2019
ms.locfileid: "75210228"
---
# <a name="creating-and-using-driver-created-file-objects"></a>ドライバー作成ファイル オブジェクトの作成と使用


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

ドライバーで、アプリケーションから独立した i/o 要求を作成し、スタック内の次のドライバー (既定の i/o ターゲット) に送信する必要がある場合、ドライバーは独自のファイルオブジェクトを作成して閉じる必要があります。

### <a name="creating-a-file-object"></a>ファイルオブジェクトの作成

ドライバーが使用するファイルオブジェクトを作成するには、ドライバーが[**Iwdfdevice:: createwdffile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createwdffile)メソッドを呼び出す必要があります。 ドライバーが**Iwdfdevice:: CreateWdfFile**を呼び出すと、フレームワークはスタック内の次のドライバーに create 要求を送信します。 スタック内の次のドライバーは、カーネルモードまたはユーザーモードである可能性があります。

このファイルの作成要求処理は、Windows Driver Model (WDM) では異なります。 WDM では、 [**Zwcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)関数を呼び出すと、create IRP がカーネルモードスタックの最上位に送られます。 次の図は、UMDF と WDM でのファイルの作成要求処理を示しています。

![umdf と wdm でのファイル要求処理の作成](images/drvrcrtfile.gif)

[**Iwdfdevice:: CreateWdfFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createwdffile)を呼び出すと、ドライバーは、ファイルオブジェクトを作成し、デバイスの起動時に、スタック全体が開始される前に i/o 要求を送信できます。

スタック内の次のドライバーは、ファイルの作成要求を処理できるかどうか、または要求をスタックの下位に転送する必要があるかどうかを判断する必要があります。

[**Iwdfdevice:: CreateWdfFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createwdffile)を呼び出した後、ドライバーは作成操作を取り消すことができません。

## <a name="using-the-file-object"></a>File オブジェクトの使用


非同期読み取り要求をその下にある次のドライバーに送信するために、ドライバーは次のパターンを使用できます。

1.  [**Iwdfdevice:: CreateWdfFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createwdffile)を呼び出して、ファイルオブジェクトを作成します。
2.  [**Iwdfdevice:: GetDefaultIoTarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-getdefaultiotarget)を呼び出して、下位レベルのドライバーを表すインターフェイスを取得します。
3.  [**Iwdfdevice:: CreateRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createrequest)を呼び出して、書式設定されていない[**IWDFIoRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiorequest)オブジェクトを作成します。
4.  [**IWDFIoRequest:: Setcompletion callback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-setcompletioncallback)を呼び出して、i/o 要求が完了したときにフレームワークによって呼び出される[**Oncompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion)メソッドの[**irequestcallback requestcompletion**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-irequestcallbackrequestcompletion)インターフェイスを登録します。
5.  [**Iwdfiotarget:: FormatRequestForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforread)を呼び出し、 *PFile*パラメーターの[**Iwdfiotarget ファイル**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdrivercreatedfile)インターフェイスへのポインターを提供します。
6.  [**IWDFIoRequest:: send**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-send)を呼び出して、要求を送信します。

## <a name="closing-the-file-object"></a>ファイルオブジェクトを閉じる


[**Iwdfdevice:: createwdffile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createwdffile)という名前のドライバーは、後で[**Iwdfdriverokfile:: Close**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdrivercreatedfile-close)を呼び出す必要があります。

通常、ドライバーは、 [**IPnpCallbackHardware:: OnReleaseHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onreleasehardware)または[**IPnpCallbackSelfManagedIo:: OnSelfManagedIoCleanup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackselfmanagedio-onselfmanagediocleanup)コールバックメソッドから[**iwdfdriverを**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdrivercreatedfile-close)呼び出します。

ドライバーが[**IwdfdriverIFileCallbackCleanup file:: Close**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdrivercreatedfile-close)を呼び出すと、フレームワークは次のドライバーの[**:: oncleanupfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackcleanup-oncleanupfile)メソッドを呼び出します。 この方法では、次のドライバーは、ファイルオブジェクトに関連付けられているすべての保留中の i/o 要求をキャンセルまたは完了する必要があります。 次に、 [**Iwdfdevice:: CreateWdfFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfdevice-createwdffile)というドライバーによって作成されたすべての i/o 要求をキャンセルします。 このフレームワークでは、スタック内の下位のドライバーがファイルオブジェクトに関連付けられている可能性がある i/o 要求はキャンセルされません。 このような要求をキャンセルするのは、ドライバーの役割です。 ファイルオブジェクトは、関連付けられているすべての i/o 要求が完了した後にのみ閉じます。

次に、フレームワークは次のドライバーの[**IFileCallbackClose:: OnCloseFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackclose-onclosefile)メソッドを呼び出します。 この時点で、フレームワークは、次のドライバーがこのファイルオブジェクトに対して追加の i/o 要求を受信しないことを保証します。

フレームワークは[**Onclosefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackclose-onclosefile)を呼び出すと、ファイルオブジェクトを表す[iwdffile](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdffile)インターフェイスを破棄します。

ドライバーによって作成されたデバイスの削除方法 ( [**IPnpCallbackHardware:: OnReleaseHardware**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onreleasehardware)や[**IPnpCallbackSelfManagedIo:: OnSelfManagedIoCleanup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackselfmanagedio-onselfmanagediocleanup)など) の後にドライバーによって作成されたファイルオブジェクトが返された場合は、フレームワークによってドライバーの停止が生成されます。 この問題のトラブルシューティングの詳細については、「 [UMDF が未解決のファイルをデバイスの削除時に示し](determining-why-umdf-indicates-outstanding-files-at-device-removal-tim.md)ている理由を特定する」を参照してください。

 

 





