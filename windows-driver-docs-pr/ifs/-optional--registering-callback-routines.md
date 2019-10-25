---
title: Optional登録 (コールバックルーチンを)
description: Optional登録 (コールバックルーチンを)
ms.assetid: 59d15b37-e31e-45fc-bdb0-fed6f791839c
keywords:
- 登録 (コールバックルーチンを)
- コールバックルーチン WDK ファイルシステム
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eeb9552cd4a9985fdd6c37f258a848f8f1ef1ab2
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841519"
---
# <a name="optional-registering-callback-routines"></a>\[オプション\] コールバックルーチンの登録


## <span id="ddk_registering_callback_routines_if"></span><span id="DDK_REGISTERING_CALLBACK_ROUTINES_IF"></span>


フィルタードライバーは、 [**IoRegisterFsRegistrationChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ioregisterfsregistrationchange)を呼び出して、ファイルシステムドライバーが[**IoRegisterFileSystem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ioregisterfilesystem)または[**iounregisterfilesystem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iounregisterfilesystem)を呼び出して自身を登録または登録解除するたびに呼び出されるコールバックルーチンを登録できます。 フィルタードライバーこのコールバックルーチンを登録すると、新しいファイルシステムにシステムを入力し、アタッチするかどうかを選択できます。

**注**   ファイルシステムフィルタードライバーは、 [**IoRegisterFileSystem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ioregisterfilesystem)または[**iounregisterfilesystem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iounregisterfilesystem)を呼び出すことはできません。 これらのルーチンは、ファイルシステム専用です。

 

明示的に指示された場合 (ユーザーモードアプリケーションなど) にのみボリュームにアタッチするフィルタードライバーは、 [**IoRegisterFsRegistrationChange**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ioregisterfsregistrationchange)を呼び出すことはできません。 ただし、このルーチンを使用するフィルターは、そのボリュームがマウントされた直後に任意のボリュームにアタッチすることができます。 このルーチンを使用しても、フィルターが直接ボリュームデバイスオブジェクトにアタッチされるとは限りません。 ただし、このようなフィルターは、現在のファイルシステムボリュームのデバイススタックの最上位にしか接続できないため、ユーザーモードアプリケーションからのコマンドを待機するフィルターの前 (およびその下) にアタッチされることを保証します。

 

 




