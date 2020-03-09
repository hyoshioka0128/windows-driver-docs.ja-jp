---
title: ボリュームの認識方法
description: ボリュームの認識方法
ms.assetid: 0531b023-f35c-4fe9-9c0d-5acafc42f9b4
keywords:
- フィルタードライバー WDK ファイルシステム、ボリュームマウントプロセス、ボリュームの認識
- ファイルシステムフィルタードライバー WDK、ボリュームマウントプロセス、ボリュームの認識
- ボリューム WDK ファイルシステム、マウント
- ボリュームのマウント (WDK ファイルシステム)
ms.date: 10/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5c70a05f7d9e8cacae2ef4fece6d45a6b830a6a3
ms.sourcegitcommit: 8c898615009705db7633649a51bef27a25d72b26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/07/2020
ms.locfileid: "78910527"
---
# <a name="how-the-volume-is-recognized"></a>ボリュームの認識方法

> [!NOTE]
> 最適な信頼性とパフォーマンスを得るには、従来のファイルシステムフィルタードライバーではなく、フィルターマネージャーをサポートする[ファイルシステムミニフィルタードライバー](https://docs.microsoft.com/windows-hardware/drivers/ifs/filter-manager-concepts)を使用します。 レガシドライバーをミニフィルタードライバーに移植する方法については、「[レガシフィルタードライバーを移植するためのガイドライン](guidelines-for-porting-legacy-filter-drivers.md)」を参照してください。

ボリュームマウントプロセスは、通常、次のように論理ボリューム (つまりパーティションまたはダイナミックボリューム) 上のファイルを開く要求によってトリガーされます。

1. ユーザーアプリケーションは、 **CreateFile**を呼び出してファイルを開きます。 またはカーネルモードドライバーは、 [**Zwcreatefile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)または[**Iocreatefilthint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)を呼び出します。

2. I/o マネージャーは、どの論理ボリュームが要求のターゲットであるかを判断し、そのデバイスオブジェクトがマウントされているかどうかを確認します。 VPB_MOUNTED フラグが設定されている場合は、ファイルシステムによってボリュームがマウントされています。

3. システムブート以降にファイルシステムによってボリュームがマウントされていない場合 (つまり、VPB_MOUNTED フラグが設定されていない場合)、i/o マネージャーは、ボリュームを要求する可能性のある各ファイルシステムにボリュームマウント ([**IRP_MJ_FILE_SYSTEM_CONTROL**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-file-system-control)、IRP_MN_MOUNT_VOLUME) 要求を送信します。

   システムを起動した後でも、すべての組み込みファイルシステムが読み込まれるとは限りません。 (「[システムブート中のファイルシステムの動作」を](what-happens-to-file-systems-during-system-boot.md)参照してください)。まだ読み込まれていない組み込みのファイルシステムの場合、i/o マネージャーはボリュームマウント要求をファイルシステムレコグナイザー (FsRec) に送信します。これにより、これらのファイルシステムに代わってボリュームブートセクターがチェックされます。

   まだ読み込まれていないファイルシステムによってボリュームがフォーマットされたことが FsRec によって判断された場合、i/o マネージャーは、ファイルシステムを読み込む読み込みファイルシステム ([**IRP_MJ_FILE_SYSTEM_CONTROL**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-file-system-control)、IRP_MN_LOAD_FILE_SYSTEM) 要求を fsrec に送信することによって応答します。 その後、i/o マネージャーが元のボリュームマウント要求をファイルシステムに送信します。

4. ボリュームのマウント要求を受信する各ファイルシステムは、ボリュームのブートセクターを調べて、ボリュームの形式とその他の情報がその特定のファイルシステムでフォーマットされたことを示しているかどうかを判断します。 形式が一致すると、ファイルシステムによってボリュームがマウントされます。

次のセクションでは、ファイルシステムが認識した後にボリュームをマウントする方法について説明します。

[ボリュームのマウント方法](how-the-volume-is-mounted.md)

[ボリュームマウントの例](volume-mount-example.md)
