---
title: システム起動時のファイル システムの状態
description: システム起動時のファイル システムの状態
ms.assetid: f6ed556a-2353-4a0d-8db1-1fb5eac3c1ef
keywords:
- フィルター ドライバー WDK ファイル システム、起動プロセス
- ファイル システム フィルター ドライバー WDK、ブート プロセス
- ファイル システム ドライバー WDK、ブート プロセス
- ファイル システムの認識エンジン WDK
- FsRec WDK
- フィルター ドライバー WDK ファイル システム、ドライバーの読み込み
- ファイル システム フィルター ドライバー WDK、ドライバーの読み込み
- ドライバー WDK ファイル システムの読み込み
- ドライバー WDK ファイル システムの読み込み
- 注文グループ WDK ファイル システムを読み込む
- ファイル システムの再初期化ルーチン WDK
- ブート ドライバー WDK ファイル システム
- ブート開始ドライバー WDK ファイル システム
- グローバルなファイル システム キュー WDK ファイル システム
- ファイル システム キュー WDK
- キューの WDK ファイル システム
- FsRec
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbf1c7cda65b48926cc824980c8a694a5b1f3f7c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380250"
---
# <a name="what-happens-to-file-systems-during-system-boot"></a>システム起動時のファイル システムの状態


## <span id="ddk_what_happens_to_file_systems_during_system_boot_if"></span><span id="DDK_WHAT_HAPPENS_TO_FILE_SYSTEMS_DURING_SYSTEM_BOOT_IF"></span>


ファイル システムは、システムのブート プロセス中に初期化されます。I/O システムを初期化具体的には中します。 I/O マネージャーは、グローバルなファイル システムのキューを作成し、PnP マネージャーと、オペレーティング システム (OS) ローダーによって読み込まれたファイル システムとフィルター ドライバーを初期化します。

ファイル システムおよびフィルター ドライバーの開発者に関心のあるシステムのブート プロセスの選択した部分の概要を次に示します。

1.  ブート ファイル システム、RAW ファイル システム、およびサービスの種類のすべてのドライバー、システムのブート時に、OS ローダーを読み込みます\_ブート\_ローダー、カーネルに制御を転送する前に開始します。 カーネルは、コントロールが取得されるメモリ内でこれらのドライバー。

    ドライバーは、割り当てられているロード順序グループの順序で読み込まれます。 ファイル システム フィルターなどの間で、新しいファイル システム フィルター ドライバーのいずれかに割り当てられているものは、グループが他のすべてのフィルター ドライバーの前に読み込まれる順序を読み込みます。 これらのロード順序グループがで詳しく説明されている[順序グループをファイル システム フィルター ドライバーの読み込み](load-order-groups-for-file-system-filter-drivers.md)します。

    [フィルター] のロード順序グループのすべてのドライバーが読み込まれます。 [フィルター] グループには、記憶域フィルター ドライバーとファイル システム フィルター ドライバーが含まれています、サード パーティだけでなく組み込みのフィルター ドライバーが含まれて ことに注意してください。

2.  I/O マネージャーは、4 つのセグメントを持つグローバル ファイル システムのキューを作成します: CD-ROM、ディスク、テープ デバイス、およびネットワーク ファイル システムに対して 1 つずつです。 後で、各ファイル システムが登録されている場合は、そのコントロールのデバイス オブジェクトがこのキューの適切なセグメントに追加されます。 この時点では、ただし、ファイル システムがまだ登録されていないので、キューは空です。

3.  PnP マネージャー呼び出し、 [ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize) RAW のルーチンはファイル システムとすべてのサービスの\_ブート\_開始ドライバー。

    場合、サービス\_ブート\_開始ドライバーはその他のドライバーに依存して、それらのドライバーが読み込まれも開始します。

    PnP マネージャーは、呼び出すことで、ブート デバイスを起動、 [ **AddDevice** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)ブート デバイス ドライバーのルーチンです。 ブート デバイスに子デバイスがある場合は、これらのデバイスが列挙されます。 子デバイスは構成およびそのドライバーがブート開始ドライバーの場合は、開始します。 デバイスのドライバーはすべてのブート開始ドライバーではない場合、PnP マネージャーは、デバイスの devnode を作成しますが、デバイスが起動しません。

    この時点では、すべてのブート ドライバーが読み込まれ、ブート デバイスが開始されます。

4.  PnP マネージャーは、検索し、各 devnode に関連付けられているドライバーの読み込みがまだ実行されていない、PnP デバイス ツリーを走査します。

    (PnP デバイス ツリーに関する詳細については、次を参照してください[デバイス ツリー](https://docs.microsoft.com/windows-hardware/drivers/kernel/device-tree)。)。各 PnP デバイスの起動時、PnP マネージャーは、存在する場合、デバイスの子を列挙します。 PnP マネージャーは、子デバイスを構成、それらのデバイス ドライバーをロードし、デバイスを開始します。

    PnP マネージャーは、各デバイスのドライバーを読み込む*かに関係なく*のドライバーの**StartType**、 **LoadOrderGroup**、または**依存関係**値。

    この手順で、PnP マネージャーのみ構成し、開始されるデバイスは PnP 列挙可能な。 デバイスが PnP 列挙可能な PnP マネージャーでは、デバイスを無視すると子デバイスがある場合でも、その子を列挙できません PnP 列挙可能な。

5.  PnP マネージャーのロードし、サービスの種類のドライバーを初期化\_システム\_まだ読み込まれていない開始します。

    ファイル システムの認識 (FsRec) は、この時点で読み込まれます。 "Boot File System"ロード順序グループではできますが、FsRec システムではない、ブート ファイルに注意してください。 実際のブート ファイル システム −、− ブート ボリュームをマウント ファイル システムがブート プロセスの開始時に読み込まれます。

    サービスの後半\_システム\_開始フェーズでは、"File System"ロード順序グループ内のファイル システムが読み込まれます。 これは、"メール スロット"ファイル システム (MSFS)、名前付きパイプ ファイル システム (NPFS) が含まれます。 これは、NTFS、FAT、cdfs を含む、UDF などのメディア ベースのファイル システムには含まれません。

    「ネットワーク」ロード順序グループでは、ネットワーク ファイル システムは、このフェーズ中にも読み込まれます。

6.  ブート時に読み込まれるすべてのドライバーが初期化された後、I/O マネージャーが設定されているすべてのドライバーの再初期化ルーチンを呼び出します。 A*再初期化ルーチン*追加を指定する必要があるブート ドライバーによって登録されているコールバック ルーチンが時間はこの時点で、ブート プロセスを処理します。 再初期化ルーチンを呼び出すことによって登録されて[ **IoRegisterBootDriverReinitialization** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioregisterbootdriverreinitialization)または[ **IoRegisterDriverReinitialization** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-ioregisterdriverreinitialization).

7.  サービス コントロール マネージャーは、サービスの種類のドライバーを読み込む\_自動\_スタートには、既に読み込まれていません。

### <a name="span-idddkfilesystemrecognizerifspanspan-idddkfilesystemrecognizerifspanfile-system-recognizer"></a><span id="ddk_file_system_recognizer_if"></span><span id="DDK_FILE_SYSTEM_RECOGNIZER_IF"></span>ファイル システムの認識

システムの起動後に、システムに接続されているすべてのボリュームの記憶装置デバイス ドライバーが読み込まれ、起動します。 ただし、すべての組み込みのファイル システムが読み込まれ、すべてのファイル システム ボリュームがマウントされています。 ファイル システムの認識 (FsRec) が処理を必要に応じて、これらのタスクを実行[ **IRP\_MJ\_作成**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)要求。

サービスで FsRec が読み込まれる\_システム\_システムの起動時のフェーズを開始します。 "Boot File System"ロード順序グループではできますが、FsRec システムではない、ブート ファイルに注意してください。 実際のブート ファイル システム −、− ブート ボリュームをマウント ファイル システムがブート プロセスの開始時に読み込まれます。

 

 




