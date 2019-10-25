---
title: ボリュームのマウント
description: ボリュームのマウント
ms.assetid: 0531b023-f35c-4fe9-9c0d-5acafc42f9b4
keywords:
- フィルタードライバー WDK ファイルシステム、ボリュームマウントプロセス
- ファイルシステムフィルタードライバー WDK、ボリュームマウントプロセス
- ボリューム WDK ファイルシステム、マウント
- ボリュームのマウント (WDK ファイルシステム)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f38e0dddcc2cffeac40a0d3a9615253cb7e1860
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841118"
---
# <a name="mounting-a-volume"></a>ボリュームのマウント


## <span id="ddk_mounting_a_volume_if"></span><span id="DDK_MOUNTING_A_VOLUME_IF"></span>


ボリュームマウントプロセスは、通常、次のように論理ボリューム (つまりパーティションまたはダイナミックボリューム) 上のファイルを開く要求によってトリガーされます。

1.  ユーザーアプリケーションは、 **CreateFile**を呼び出してファイルを開きます。 またはカーネルモードドライバーは、 [**Zwcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)または[**Iocreatefilthint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)を呼び出します。

2.  I/o マネージャーは、どの論理ボリュームが要求のターゲットであるかを判断し、そのデバイスオブジェクトがマウントされているかどうかを確認します。 VPB\_マウントフラグが設定されている場合は、ファイルシステムによってボリュームがマウントされています。

3.  システムブート以降にファイルシステムによってボリュームがマウントされていない場合 (つまり、VPB\_マウントされたフラグが設定されていない場合)、i/o マネージャーはボリュームマウント ([**IRP\_MJ\_ファイル\_システム\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-file-system-control)に送信します。、IRP\_、ボリュームを要求する可能性のある各ファイルシステムに対して、\_MOUNT\_VOLUME) 要求を行います。

    システムを起動した後でも、すべての組み込みファイルシステムが読み込まれるとは限りません。 (「[システムブート中のファイルシステムの動作」を](what-happens-to-file-systems-during-system-boot.md)参照してください)。まだ読み込まれていない組み込みのファイルシステムの場合、i/o マネージャーはボリュームマウント要求をファイルシステムレコグナイザー (FsRec) に送信します。これにより、これらのファイルシステムに代わってボリュームブートセクターがチェックされます。

    まだ読み込まれていないファイルシステムによってボリュームがフォーマットされたことが FsRec によって判断された場合、i/o マネージャーは、負荷ファイルシステム ([**irp\_MJ\_ファイル\_システム\_制御**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-file-system-control)、irp\_完了\_読み込み\_ファイルを送信することによって応答します。\_システム) を FsRec に要求します。これにより、ファイルシステムが読み込まれます。 その後、i/o マネージャーが元のボリュームマウント要求をファイルシステムに送信します。

4.  ボリュームのマウント要求を受信する各ファイルシステムは、ボリュームのブートセクターを調べて、ボリュームの形式とその他の情報がその特定のファイルシステムでフォーマットされたことを示しているかどうかを判断します。 形式が一致すると、ファイルシステムによってボリュームがマウントされます。

次のセクションでは、ファイルシステムが認識した後にボリュームをマウントする方法について説明します。

[ボリュームのマウント方法](how-the-volume-is-mounted.md)

[ボリュームマウントの例](volume-mount-example.md)

 

 




