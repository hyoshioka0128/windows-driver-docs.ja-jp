---
title: 作成して、ドライバーに作成されたファイル オブジェクトを使用します。
description: 作成して、ドライバーに作成されたファイル オブジェクトを使用します。
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
ms.openlocfilehash: 6ca6e7a6e717d78b4c938b0fc056188874f40d59
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56560092"
---
# <a name="creating-and-using-driver-created-file-objects"></a>作成して、ドライバーに作成されたファイル オブジェクトを使用します。


[!include[UMDF 1 Deprecation](../umdf-1-deprecation.md)]

ドライバーは、作成しの 次へ のドライバー スタック (既定の I/O ターゲット) にアプリケーションから独立している I/O 要求を送信する必要があります、ドライバーでを作成し、独自のファイル オブジェクトを閉じる必要があります。

### <a name="creating-a-file-object"></a>ファイル オブジェクトを作成します。

ドライバーを呼び出す必要があります、 [ **IWDFDevice::CreateWdfFile** ](https://msdn.microsoft.com/library/windows/hardware/ff558828)ドライバーの使用するためのファイル オブジェクトを作成します。 ドライバーを呼び出すと**IWDFDevice::CreateWdfFile**フレームワークでは、要求の作成をスタック内の次のドライバーに送信します。 カーネル モードまたはユーザー モードで、次のドライバー スタックの可能性があります。

このファイルの作成要求の処理は、Windows Driver Model (WDM) で異なります。 WDM への呼び出しで、 [ **ZwCreateFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566424)関数により作成 IRP、カーネル モード スタックの一番上に移動します。 次の図では、UMDF WDM とでファイルの作成要求の処理を示しています。

![ファイルの作成要求が wdm と umdf の処理](images/drvrcrtfile.gif)

呼び出して[ **IWDFDevice::CreateWdfFile**](https://msdn.microsoft.com/library/windows/hardware/ff558828)ドライバーは、ファイル オブジェクトを作成し、スタック全体が開始する前にデバイスの起動中に I/O 要求を送信します。

スタック内の次のドライバーには、ファイルの作成要求を処理できる場合、または下位のスタックでさらに、要求を転送する必要がありますを決定する必要があります。

呼び出した後[ **IWDFDevice::CreateWdfFile**](https://msdn.microsoft.com/library/windows/hardware/ff558828)ドライバーは、作成操作を取り消すことはできません。

## <a name="using-the-file-object"></a>ファイル オブジェクトを使用します。


ドライバー積み上げ下に、次のドライバーに非同期の読み取り要求を送信するには、次のパターンを使用できます。

1.  呼び出す[ **IWDFDevice::CreateWdfFile** ](https://msdn.microsoft.com/library/windows/hardware/ff558828)ファイル オブジェクトを作成します。
2.  呼び出す[ **IWDFDevice::GetDefaultIoTarget** ](https://msdn.microsoft.com/library/windows/hardware/ff558831)下位レベルのドライバーを表すインターフェイスを取得します。
3.  呼び出す[ **IWDFDevice::CreateRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff557021)を作成、書式設定されていない[ **IWDFIoRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff558985)オブジェクト。
4.  呼び出す[ **IWDFIoRequest::SetCompletionCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff559153)を登録する、 [ **IRequestCallbackRequestCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff556904) のインターフェイス[**OnCompletion** ](https://msdn.microsoft.com/library/windows/hardware/ff556905) I/O 要求が完了したときにフレームワークから呼び出されるメソッド。
5.  呼び出す[ **IWDFIoTarget::FormatRequestForRead**](https://msdn.microsoft.com/library/windows/hardware/ff559233)へのポインターを提供する、 [ **IWDFDriverCreatedFile** ](https://msdn.microsoft.com/library/windows/hardware/ff558895) インターフェイス*pFile*パラメーター。
6.  呼び出す[ **IWDFIoRequest::Send** ](https://msdn.microsoft.com/library/windows/hardware/ff559149)要求を送信します。

## <a name="closing-the-file-object"></a>ファイル オブジェクトを閉じる


呼ばれるドライバー [ **IWDFDevice::CreateWdfFile** ](https://msdn.microsoft.com/library/windows/hardware/ff558828)後で呼び出す必要があります[ **IWDFDriverCreatedFile::Close**](https://msdn.microsoft.com/library/windows/hardware/ff558897)します。

通常、ドライバーの呼び出し[ **IWDFDriverCreatedFile::Close** ](https://msdn.microsoft.com/library/windows/hardware/ff558897)のいずれかからその[ **IPnpCallbackHardware::OnReleaseHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556768)または[ **IPnpCallbackSelfManagedIo::OnSelfManagedIoCleanup** ](https://msdn.microsoft.com/library/windows/hardware/ff556780)コールバック メソッド。

ドライバーを呼び出すと[ **IWDFDriverCreatedFile::Close**](https://msdn.microsoft.com/library/windows/hardware/ff558897)、フレームワークは、次のドライバーの[ **IFileCallbackCleanup::OnCleanupFile** ](https://msdn.microsoft.com/library/windows/hardware/ff554905)メソッド。 このメソッドは、次のドライバーがキャンセルまたは、ファイル オブジェクトに関連付けられているすべての保留中 I/O 要求を完了する必要があります。 フレームワークと呼ばれるドライバーによって作成されたすべての I/O 要求をキャンセルし[ **IWDFDevice::CreateWdfFile**](https://msdn.microsoft.com/library/windows/hardware/ff558828)します。 フレームワークでは、スタックの下位のドライバーが、ファイル オブジェクトに関連付けられているすべての I/O 要求は取り消されません。 このようなすべての要求をキャンセルするドライバーの役目です。 関連付けられているすべての I/O 要求が完了した後のみ、ファイル オブジェクトを終了します。

次に、フレームワークが、[次へ] のドライバーを呼び出す[ **IFileCallbackClose::OnCloseFile** ](https://msdn.microsoft.com/library/windows/hardware/ff554910)メソッド。 この時点では、フレームワークでは、次のドライバーは、このファイル オブジェクトの追加の I/O 要求を受け取りませんが保証されます。

Framework の呼び出し後に[ **OnCloseFile**](https://msdn.microsoft.com/library/windows/hardware/ff554910)、破棄、 [IWDFFile](https://msdn.microsoft.com/library/windows/hardware/ff558912)ファイル オブジェクトを表すインターフェイスです。

ドライバーに作成されたファイル オブジェクトが、ドライバーのデバイスの削除メソッドの後に残っている場合 (たとえば[ **IPnpCallbackHardware::OnReleaseHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556768)と[ **IPnpCallbackSelfManagedIo::OnSelfManagedIoCleanup**](https://msdn.microsoft.com/library/windows/hardware/ff556780)) 戻り、ドライバーの停止はフレームワークに生成されます。 この問題をトラブルシューティングする方法の詳細については、[を決定する理由 UMDF 示します未処理のファイルがデバイスの削除時に](determining-why-umdf-indicates-outstanding-files-at-device-removal-tim.md)を参照してください。

 

 





