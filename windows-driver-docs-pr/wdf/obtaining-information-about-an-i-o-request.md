---
title: I/O 要求に関する情報の取得
description: I/O 要求に関する情報の取得
ms.assetid: a686ea00-6987-480a-a4ce-892e1efbed87
keywords:
- 要求の処理の WDK KMDF、に関する情報を取得します。
- I/O 要求の WDK KMDF、に関する情報を取得します。
- WDK KMDF のステータス情報
- 状態は WDK KMDF、I/O 要求します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4462c2f603f5d7c6e6ce57017fe9048961c2e8f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580843"
---
# <a name="obtaining-information-about-an-io-request"></a>I/O 要求に関する情報の取得


ドライバーは、I/O 要求を処理するには、前に、要求の種類を判断する必要があります。 フレームワーク ベースのドライバーと[の I/O キューを作成します。](creating-i-o-queues.md)デバイスの場合、通常設定の I/O キューと要求ハンドラーを各キューまたは要求のハンドラーが特定の種類 (読み取り、書き込み、またはデバイスの I/O コントロール) の要求を受信できるようにします。

要求の種類を決定した後、ドライバーする必要があります取得要求の入力と出力バッファーでは、必要な場合。 要求のバッファーを取得する方法の詳細については、次を参照してください。 [Framework ベースのドライバーでのデータ バッファーへのアクセス](https://msdn.microsoft.com/library/windows/hardware/ff540701)します。

ドライバーが受信した I/O 要求に関する追加情報を提供するには、フレームワークの要求オブジェクトは、次のメソッドを定義します。

-   [**WdfRequestGetIoQueue**](https://msdn.microsoft.com/library/windows/hardware/ff549968)、I/O 要求の配信元となる I/O キューに識別するハンドルを返します。

-   [**WdfRequestGetRequestorMode**](https://msdn.microsoft.com/library/windows/hardware/ff549971)要求の発信元のプロセッサのアクセス モード (ユーザーまたはカーネル) が返されます。

-   [**WdfRequestGetFileObject**](https://msdn.microsoft.com/library/windows/hardware/ff549963)要求に関連付けられている framework ファイル オブジェクトへのハンドルを返します。

-   [**WdfRequestWdmGetIrp**](https://msdn.microsoft.com/library/windows/hardware/ff550037)、WDM を返す[ **IRP** ](https://msdn.microsoft.com/library/windows/hardware/ff550694)要求に関連付けられている構造体。

-   [**WdfRequestGetParameters**](https://msdn.microsoft.com/library/windows/hardware/ff549969)、WDM 形式で非 IRP 要求パラメーターを取得します。

ドライバー スタックの他のドライバーをドライバーには、I/O 要求が完了すると後、は、追加の要求が要求完了の情報を取得するオブジェクトのメソッドに呼び出すことができます。 これらの追加メソッドの詳細については、次を参照してください。 [I/O 要求の完了](completing-i-o-requests.md)します。

 

 





