---
title: フレームワークでサポートされていない IRP の処理
description: フレームワークでサポートされていない IRP の処理
ms.assetid: 0481f335-f63b-4f93-8eb4-523a70082302
keywords:
- サポートされていない WDM Irp の WDK KMDF
- Irp WDK KMDF、サポートされていません
- WDM Irp の WDK KMDF、サポートされていません
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6a7ab11484a4e6ab0ecb5f4202c5c4d03e7d3b5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580153"
---
# <a name="handling-an-irp-that-the-framework-does-not-support"></a>フレームワークでサポートされていない IRP の処理


\[KMDF にのみ適用されます。\]

フレームワークは、次の主要な IRP のコードの I/O 要求をサポートしません。

-   IRP\_MJ\_作成\_"メール スロット"
-   IRP\_MJ\_作成\_名前付き\_パイプ
-   IRP\_MJ\_デバイス\_変更
-   [**IRP\_MJ\_ディレクトリ\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff548658)
-   [**IRP\_MJ\_ファイル\_システム\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff550751)
-   [**IRP\_MJ\_フラッシュ\_バッファー**](https://msdn.microsoft.com/library/windows/hardware/ff550760)
-   [**IRP\_MJ\_ロック\_コントロール**](https://msdn.microsoft.com/library/windows/hardware/ff549251)
-   [**IRP\_MJ\_クエリ\_EA**](https://msdn.microsoft.com/library/windows/hardware/ff549279)
-   [**IRP\_MJ\_クエリ\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff549283)
-   [**IRP\_MJ\_クエリ\_クォータ**](https://msdn.microsoft.com/library/windows/hardware/ff549293)
-   [**IRP\_MJ\_QUERY\_SECURITY**](https://msdn.microsoft.com/library/windows/hardware/ff549298)
-   [**IRP\_MJ\_クエリ\_ボリューム\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff549318)
-   [**IRP\_MJ\_SET\_EA**](https://msdn.microsoft.com/library/windows/hardware/ff549346)
-   [**IRP\_MJ\_SET\_INFORMATION**](https://msdn.microsoft.com/library/windows/hardware/ff550799)
-   [**IRP\_MJ\_SET\_QUOTA**](https://msdn.microsoft.com/library/windows/hardware/ff549401)
-   [**IRP\_MJ\_SET\_SECURITY**](https://msdn.microsoft.com/library/windows/hardware/ff549407)
-   [**IRP\_MJ\_設定\_ボリューム\_情報**](https://msdn.microsoft.com/library/windows/hardware/ff549415)

フレームワークは、これらの I/O 関数コードのいずれかを含む IRP を受信する場合、フレームワークは IRP を処理しません。 ドライバーが、フィルター ドライバーの場合は、フレームワークは、次の下位ドライバーはドライバー スタックに IRP を渡します。 ドライバーでない場合、フィルター ドライバー、フレームワーク[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)状態のステータス値を持つ IRP の完了に\_無効な\_デバイス\_要求します。

ドライバーを呼び出す必要があります、ドライバーでは、これらの I/O 関数コードのいずれかが含まれている Irp を処理する必要がある場合[ **WdfDeviceInitAssignWdmIrpPreprocessCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff546043)を登録する、 [ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925) I/O 関数のコードのイベントのコールバック関数。

ドライバーがドライバーに登録されている I/O 関数コードを含む IRP を受信すると、 [ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)コールバックに framework パス IRP のコールバック関数関数。 コールバック関数に従って IRP を処理する必要がありますし、 [WDM Irp の取り扱いルール](https://msdn.microsoft.com/library/windows/hardware/ff546847)します。 ドライバーを呼び出す必要があります[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)完了、IRP も呼び出す必要があります[**保留**](https://msdn.microsoft.com/library/windows/hardware/ff548336) IRP を次の下位に渡すドライバー。

例については、 [ *EvtDeviceWdmIrpPreprocess* ](https://msdn.microsoft.com/library/windows/hardware/ff540925)フレームワークがサポートされていない IRP を処理するコールバック関数を参照してください、[シリアル](sample-kmdf-drivers.md)サンプル ドライバー。

 

 





