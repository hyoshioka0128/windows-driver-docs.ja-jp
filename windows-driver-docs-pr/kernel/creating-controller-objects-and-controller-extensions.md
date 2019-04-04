---
title: コントローラー オブジェクトとコントローラー拡張の作成
description: コントローラー オブジェクトとコントローラー拡張の作成
ms.assetid: 1f5bfcbc-1d8e-4ace-9539-a25e226444a6
keywords:
- コント ローラー オブジェクトの WDK カーネルを作成します。
- IoCreateController
- WDK I/O コント ローラーの拡張機能
- WDK のコント ローラー オブジェクトの拡張機能
- コント ローラー オブジェクトの WDK カーネル、拡張機能
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e08f8c4911cac4b245fdea4ddc448dbfe990e85b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56570304"
---
# <a name="creating-controller-objects-and-controller-extensions"></a>コントローラー オブジェクトとコントローラー拡張の作成





呼び出す必要がありますが、ドライバーは、コント ローラー オブジェクトを使用している場合[ **IoCreateController** ](https://msdn.microsoft.com/library/windows/hardware/ff548395)デバイス オブジェクトが作成し、そのデバイスの準備ができて I/O、通常、PnP を受け取った後[ **IRP\_MN\_開始\_デバイス**](https://msdn.microsoft.com/library/windows/hardware/ff551749)要求。 次の図は、呼び出しを示します。

![コント ローラー オブジェクトを示す図](images/3ctlrobj.png)

すべてのコント ローラー オブジェクトには、関連付けられたコント ローラーの拡張機能があります。 前の図に示すの呼び出し元**IoCreateController**決定、*サイズ*コント ローラー拡張機能の。 その構造と内容は、ドライバーで定義されます。

だけでなく任意のデバイス固有ドライバーは、物理コント ローラー (またはデバイスのチャネル)、前の図、状態情報には、コント ローラーの拡張機能のドライバーの定義済みのデータの代表的なセットが表示されます。

*PtrToControllerObject*によって返されたポインター **IoCreateController**、ドライバーの呼び出しで渡す必要がある[ **IoAllocateController** ](https://msdn.microsoft.com/library/windows/hardware/ff548224)と[ **IoFreeController**](https://msdn.microsoft.com/library/windows/hardware/ff549104)に記述されている[I/O 操作のコント ローラーのオブジェクトを割り当てる](allocating-controller-objects-for-i-o-operations.md)します。 ドライバーは、そのデバイスのドライバーが作成したオブジェクトのデバイスの拡張機能または別の常駐記憶域のドライバーにアクセス可能な領域 (非ページ プール、ドライバーによって割り当てられた) で、コント ローラーが返されるオブジェクトへのポインターを格納する必要があります。 ドライバーが読み込まれた場合は、これも渡す必要があります、コント ローラーへのオブジェクト ポインター [ **IoDeleteController**](https://msdn.microsoft.com/library/windows/hardware/ff549078)します。

コント ローラーのオブジェクトを設定するほとんどのドライバーを検索するコント ローラー拡張機能の現在のターゲット デバイス オブジェクト、またはデバイス拡張子へのポインターを格納すると便利です。 通常、このようなドライバー コント ローラー オブジェクトのポインターを保存のすべてのデバイスの拡張機能の使用できるように、 *ControllerObject * * *-&gt;ControllerExtension** ドライバーで維持されるアクセスへのポインターターゲット デバイスのすべてのオブジェクトの I/O 操作についての状態をコント ローラーに固有です。

コント ローラーのオブジェクトによって表される物理コント ローラーは、割り込みを生成する場合、ドライバーも使用できますコント ローラー拡張機能のストレージとして*PtrToInterruptObject*で返されたポインター [ **IoConnectInterrupt**](https://msdn.microsoft.com/library/windows/hardware/ff548371)します。 詳細については、[割り込みサービス ルーチン](interrupt-service-routines.md)を参照してください。

**IoCreateController**常駐ストレージ コント ローラーのオブジェクトと拡張機能は、ゼロで初期化を割り当てます。 場合は、メモリを割り当てることができません**IoCreateController**を返します、 **NULL**ポインター。 このような場合、ドライバーがデバイスのスタートアップに失敗する必要があり、状態を返す必要があります\_不十分\_リソース。

 

 




