---
title: ボリュームのマウント
description: ボリュームのマウント
ms.assetid: 0531b023-f35c-4fe9-9c0d-5acafc42f9b4
keywords:
- フィルター ドライバー WDK ファイル システムのボリュームのマウント プロセス
- ファイル システム フィルター ドライバー WDK ボリュームのマウント プロセス
- WDK ファイル システムのボリュームをマウント
- WDK のファイル システム ボリュームのマウント
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: af73e8e5235e7530f4a3fd2e66d70658173205da
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383885"
---
# <a name="mounting-a-volume"></a>ボリュームのマウント


## <span id="ddk_mounting_a_volume_if"></span><span id="DDK_MOUNTING_A_VOLUME_IF"></span>


ボリュームのマウント プロセスは、通常次のように (つまり、パーティション、またはダイナミック ボリューム) の論理ボリューム上のファイルを開く要求によってトリガーされます。

1.  ユーザーのアプリケーションを呼び出す**CreateFile**ファイルを開きます。 カーネル モード ドライバーは呼び出しまたは[ **ZwCreateFile** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-ntcreatefile)または[ **IoCreateFileSpecifyDeviceObjectHint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-iocreatefilespecifydeviceobjecthint)します。

2.  I/O マネージャーは、論理ボリュームが、要求の対象になるしがマウントされているかどうかを確認するには、そのデバイス オブジェクトをチェックを決定します。 場合、VPB\_マウント済みフラグが設定されて、ファイル システムで、ボリュームがマウントされています。

3.  かどうか、ボリュームがシステムの起動後のファイル システムとしてマウントされていません (VPB、\_マウント済みフラグが設定されていない)、ボリュームのマウントを送信する I/O マネージャー ([**IRP\_MJ\_ファイル\_システム\_コントロール**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-file-system-control)、IRP\_MN\_マウント\_ボリューム) が要求のボリュームごとのファイル システムに要求します。

    すべての組み込みのファイル システムは、システムのブート後でも、− を必ずしも読み込まれます。 (を参照してください[システム ブート時にファイル システムに起こる](what-happens-to-file-systems-during-system-boot.md))。まだ読み込まれていない組み込みのファイル システムでは、I/O マネージャーは、ファイル システム認識エンジンに対する (FsRec) に代わって、これらのファイル システム ボリュームのブート セクターをチェックするボリュームのマウント要求を送信します。

    I/O マネージャーに負荷のファイル システムに送信することによって応答 FsRec ボリュームがまだ読み込まれていないファイル システムでフォーマットされていると判断した場合 ([**IRP\_MJ\_ファイル\_システム\_コントロール** ](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-file-system-control)、IRP\_MN\_ロード\_ファイル\_システム) 要求を FsRec で、ファイル システムを読み込みます。 次に、I/O マネージャーはファイル システムに元のボリュームのマウント要求を送信します。

4.  各ファイル システム ボリュームのマウント要求を受信するかどうか、ボリュームのフォーマットとその他の情報を示す、ボリュームがその特定のファイル システムでフォーマットされたことを確認するボリュームのブート セクターを調べます。 形式が一致すると、ファイル システムは、ボリュームをマウントします。

次のセクションでは、ファイル システムがそれを認識した後、ボリュームをマウントする方法について説明します。

[ボリュームをマウントする方法](how-the-volume-is-mounted.md)

[ボリューム マウントの例](volume-mount-example.md)

 

 




