---
title: ドライバー作成ファイル オブジェクトの作成と使用
description: ドライバー作成ファイル オブジェクトの作成と使用
ms.assetid: 84b677b4-fddf-4f06-9ea6-e4642c3f1b2d
keywords:
- ドライバーに作成されたファイル オブジェクト WDK UMDF
- ドライバーに作成されたファイル オブジェクトの作成と使用の WDK UMDF
- I/O WDK の UMDF ドライバー-作成されたときに、ハンドルが作成、および使用するファイル オブジェクト
- I/O 要求の WDK UMDF、ファイルのオブジェクトの作成と使用
- ユーザー モード ドライバー フレームワーク WDK、ファイル オブジェクトの作成と使用の I/O ハンドルを
- UMDF WDK、ファイル オブジェクトの作成と使用の I/O ハンドルを
- ユーザー モード ドライバー WDK UMDF、ファイル オブジェクトの作成と使用の I/O ハンドルを
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 252089bc68f053ca823bd7bd7dce7717789023fa
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382409"
---
# <a name="creating-and-using-driver-created-file-objects"></a>ドライバー作成ファイル オブジェクトの作成と使用


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ドライバーは、作成しの 次へ のドライバー スタック (既定の I/O ターゲット) にアプリケーションから独立している I/O 要求を送信する必要があります、ドライバーでを作成し、独自のファイル オブジェクトを閉じる必要があります。

### <a name="creating-a-file-object"></a>ファイル オブジェクトを作成します。

ドライバーを呼び出す必要があります、 [ **IWDFDevice::CreateWdfFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-createwdffile)ドライバーの使用するためのファイル オブジェクトを作成します。 ドライバーを呼び出すと**IWDFDevice::CreateWdfFile**フレームワークでは、要求の作成をスタック内の次のドライバーに送信します。 カーネル モードまたはユーザー モードで、次のドライバー スタックの可能性があります。

このファイルの作成要求の処理は、Windows Driver Model (WDM) で異なります。 WDM への呼び出しで、 [ **ZwCreateFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)関数により作成 IRP、カーネル モード スタックの一番上に移動します。 次の図では、UMDF WDM とでファイルの作成要求の処理を示しています。

![ファイルの作成要求が wdm と umdf の処理](images/drvrcrtfile.gif)

呼び出して[ **IWDFDevice::CreateWdfFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-createwdffile)ドライバーは、ファイル オブジェクトを作成し、スタック全体が開始する前にデバイスの起動中に I/O 要求を送信します。

スタック内の次のドライバーには、ファイルの作成要求を処理できる場合、または下位のスタックでさらに、要求を転送する必要がありますを決定する必要があります。

呼び出した後[ **IWDFDevice::CreateWdfFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-createwdffile)ドライバーは、作成操作を取り消すことはできません。

## <a name="using-the-file-object"></a>ファイル オブジェクトを使用します。


ドライバー積み上げ下に、次のドライバーに非同期の読み取り要求を送信するには、次のパターンを使用できます。

1.  呼び出す[ **IWDFDevice::CreateWdfFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-createwdffile)ファイル オブジェクトを作成します。
2.  呼び出す[ **IWDFDevice::GetDefaultIoTarget** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-getdefaultiotarget)下位レベルのドライバーを表すインターフェイスを取得します。
3.  呼び出す[ **IWDFDevice::CreateRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-createrequest)を作成、書式設定されていない[ **IWDFIoRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfiorequest)オブジェクト。
4.  呼び出す[ **IWDFIoRequest::SetCompletionCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-setcompletioncallback)を登録する、 [ **IRequestCallbackRequestCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-irequestcallbackrequestcompletion) のインターフェイス[**OnCompletion** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-irequestcallbackrequestcompletion-oncompletion) I/O 要求が完了したときにフレームワークから呼び出されるメソッド。
5.  呼び出す[ **IWDFIoTarget::FormatRequestForRead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiotarget-formatrequestforread)へのポインターを提供する、 [ **IWDFDriverCreatedFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdfdrivercreatedfile) インターフェイス*pFile*パラメーター。
6.  呼び出す[ **IWDFIoRequest::Send** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfiorequest-send)要求を送信します。

## <a name="closing-the-file-object"></a>ファイル オブジェクトを閉じる


呼ばれるドライバー [ **IWDFDevice::CreateWdfFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-createwdffile)後で呼び出す必要があります[ **IWDFDriverCreatedFile::Close**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdrivercreatedfile-close)します。

通常、ドライバーの呼び出し[ **IWDFDriverCreatedFile::Close** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdrivercreatedfile-close)のいずれかからその[ **IPnpCallbackHardware::OnReleaseHardware** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackhardware-onreleasehardware)または[ **IPnpCallbackSelfManagedIo::OnSelfManagedIoCleanup** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackselfmanagedio-onselfmanagediocleanup)コールバック メソッド。

ドライバーを呼び出すと[ **IWDFDriverCreatedFile::Close**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdrivercreatedfile-close)、フレームワークは、次のドライバーの[ **IFileCallbackCleanup::OnCleanupFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ifilecallbackcleanup-oncleanupfile)メソッド。 このメソッドは、次のドライバーがキャンセルまたは、ファイル オブジェクトに関連付けられているすべての保留中 I/O 要求を完了する必要があります。 フレームワークと呼ばれるドライバーによって作成されたすべての I/O 要求をキャンセルし[ **IWDFDevice::CreateWdfFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-iwdfdevice-createwdffile)します。 フレームワークでは、スタックの下位のドライバーが、ファイル オブジェクトに関連付けられているすべての I/O 要求は取り消されません。 このようなすべての要求をキャンセルするドライバーの役目です。 関連付けられているすべての I/O 要求が完了した後のみ、ファイル オブジェクトを終了します。

次に、フレームワークが、[次へ] のドライバーを呼び出す[ **IFileCallbackClose::OnCloseFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ifilecallbackclose-onclosefile)メソッド。 この時点では、フレームワークでは、次のドライバーは、このファイル オブジェクトの追加の I/O 要求を受け取りませんが保証されます。

Framework の呼び出し後に[ **OnCloseFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ifilecallbackclose-onclosefile)、破棄、 [IWDFFile](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-iwdffile)ファイル オブジェクトを表すインターフェイスです。

ドライバーに作成されたファイル オブジェクトが、ドライバーのデバイスの削除メソッドの後に残っている場合 (たとえば[ **IPnpCallbackHardware::OnReleaseHardware** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackhardware-onreleasehardware)と[ **IPnpCallbackSelfManagedIo::OnSelfManagedIoCleanup**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallbackselfmanagedio-onselfmanagediocleanup)) 戻り、ドライバーの停止はフレームワークに生成されます。 この問題をトラブルシューティングする方法の詳細については、次を参照してください。[を決定する理由 UMDF 示します未処理のファイルがデバイスの削除時に](determining-why-umdf-indicates-outstanding-files-at-device-removal-tim.md)します。

 

 





