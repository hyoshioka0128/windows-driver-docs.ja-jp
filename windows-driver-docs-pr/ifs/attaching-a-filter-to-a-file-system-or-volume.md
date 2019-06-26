---
title: ファイル システムまたはボリュームへのフィルターのアタッチ
description: ファイル システムまたはボリュームへのフィルターのアタッチ
ms.assetid: 7c5059b3-cd9f-4a83-8f78-5a2fcc96b246
keywords:
- フィルターをアタッチ、フィルター ドライバー WDK ファイル システム
- ファイル システム フィルター ドライバー WDK、フィルターをアタッチします。
- ファイル システムまたはボリュームにフィルターをアタッチします。
- WDK のボリュームのファイル システム、フィルターをアタッチします。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4b0cda49c9fe05a38cec7c293511212eee6558b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375732"
---
# <a name="attaching-a-filter-to-a-file-system-or-volume"></a>ファイル システムまたはボリュームへのフィルターのアタッチ


## <span id="ddk_attaching_a_filter_to_a_file_system_or_volume_if"></span><span id="DDK_ATTACHING_A_FILTER_TO_A_FILE_SYSTEM_OR_VOLUME_IF"></span>


ファイル システム フィルター ドライバーは自体を 1 つまたは複数のマウントされたボリュームにアタッチし、それらのすべての I/O 操作をフィルターします。 しかし、それ自体をアタッチするには、どのボリュームを決定方法はでしょうか。 サンプルのフィルター ドライバー、Windows Driver Kit (WDK) では、実行は、この 2 つの最も一般的な方法を示しています。

-   エンド ユーザーでは、フィルター処理にボリュームをたとえば、指定するため、ボリュームのドライブ文字を入力します。 エンドユーザーのコマンドは、プライベートとしてフィルター ドライバーに中継[ **IRP\_MJ\_デバイス\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-device-control)要求。

-   ファイル システム フィルター ドライバーが 1 つまたは複数のファイル システム ドライバーをアタッチ、リッスン[ **IRP\_MJ\_ファイル\_システム\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-file-system-control)、IRP\_MN\_マウント\_ボリュームの要求とは、マウントされたボリュームに接続します。

**注**  ドライブ文字をボリュームのマッピングは、1 対多、一対一しないことを想定してください一般にします。 これは、ダイナミック ボリュームとボリュームのマウント ポイントなど、高度なストレージ機能のためです。

 

**注**  想定しないでくださいその IRP\_MN\_マウント\_ボリューム要求がファイル システムで同期的に処理が常にします。 たとえば、フロッピー ドライブは、ドライブにフロッピー ディスクがない場合、非同期的にマウントすることがあります。 したがって、フィルター ドライバーを準備を伝達する必要があります、 **PendingReturned**そのマウント完了ルーチンのフラグ。 詳細については、次を参照してください"[PendingReturned フラグ](checking-the-pendingreturned-flag.md)。"。

 

ファイル システム フィルター ドライバーにアタッチし、任意のファイル システム ボリュームの I/O をフィルター処理できます。 これらは、ディスク ドライブやパーティションなどの記憶装置に直接アタッチできません。 また、個々 のディレクトリまたはファイルに、アタッチできません。

詳しくは、次のトピックをご覧ください。

[フィルターのデバイス オブジェクトを作成します。](creating-the-filter-device-object.md)

[ターゲット デバイスのオブジェクトへのフィルターのデバイス オブジェクトのアタッチ](attaching-the-filter-device-object-to-the-target-device-object.md)

[メッセージを伝達する\_バッファーに格納された\_IO、および DO\_直接\_IO フラグ](propagating-the-do-buffered-io-and-do-direct-io-flags.md)

[ファイルを伝達する\_デバイス\_SECURE\_オープン フラグ](propagating-the-file-device-secure-open-flag.md)

[オフ\_デバイス\_初期化フラグ](clearing-the-do-device-initializing-flag.md)

 

 




