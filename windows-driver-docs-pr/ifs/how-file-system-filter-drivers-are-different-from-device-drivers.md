---
title: ファイル システム フィルター ドライバーとデバイス ドライバーの相違点
description: ファイル システム フィルター ドライバーとデバイス ドライバーの相違点
ms.assetid: 64a59564-a4d7-4174-82d3-60bd1a30b2d8
keywords:
- フィルタードライバー WDK ファイルシステム、およびデバイスドライバー
- ファイルシステムフィルタードライバー WDK、およびデバイスドライバー
- デバイスドライバー WDK ファイルシステム
ms.date: 10/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: 82363ccc6c500d8132989dbdaf726138b8115387
ms.sourcegitcommit: 2a1c24db881ed843498001493c3ce202c9aa03f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2019
ms.locfileid: "74128490"
---
# <a name="how-file-system-filter-drivers-are-different-from-device-drivers"></a>ファイル システム フィルター ドライバーとデバイス ドライバーの相違点

Microsoft Windows オペレーティングシステムのファイルシステムフィルタードライバーとデバイスドライバーは、次の点で異なります。

- **電源管理なし**

  ファイルシステムフィルタードライバーはデバイスドライバーではないため、ハードウェアデバイスを直接制御しないため、 [**IRP\_MJ\_の電源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-power)要求を受信しません。 代わりに、電力 Irp はストレージデバイススタックに直接送信されます。 ただし、まれに、ファイルシステムフィルタードライバーによって電源管理が妨げられることがあります。 このため、ファイルシステムフィルタードライバーは、 **Driverentry**ルーチンで IRP\_MJ\_電源のディスパッチルーチンを登録する必要がありません。また、 [poxxx](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)ルーチンを呼び出すことはできません。

- **WDM なし**

  ファイルシステムフィルタードライバーを Windows Driver Model (WDM) ドライバーにすることはできません。 Microsoft [Windows Driver Model](https://docs.microsoft.com/windows-hardware/drivers/kernel/windows-driver-model)は、デバイスドライバーのみを対象としています。

- **AddDevice または StartIo はありません**

  ファイルシステムフィルタードライバーはデバイスドライバーではないため、ハードウェアデバイスを直接制御しないので、 [**AddDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)または[**StartIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)ルーチンを指定しないでください。

- **作成されたさまざまなデバイスオブジェクト**

  ファイルシステムフィルタードライバーとデバイスドライバーは両方ともデバイスオブジェクトを作成しますが、作成するデバイスオブジェクトの数と種類は異なります。

  デバイスドライバーは、デバイスを表す物理デバイスオブジェクトと機能デバイスオブジェクトを作成します。 プラグアンドプレイ (PnP) マネージャーは、デバイスドライバーによって作成されたすべてのデバイスオブジェクトを含むグローバルデバイスツリーを構築し、管理します。 ファイルシステムフィルタードライバーによって作成されたデバイスオブジェクトは、このデバイスツリーに含まれていません。

  ファイルシステムフィルタードライバーは、物理的または機能しているデバイスオブジェクトを作成しません。 代わりに、コントロールデバイスオブジェクトを作成し、デバイスオブジェクトをフィルター処理します。 *コントロールデバイスオブジェクト*は、システムおよびユーザーモードアプリケーションに対するフィルタードライバーを表します。 *フィルターデバイスオブジェクト*は、特定のファイルシステムまたはボリュームをフィルター処理する実際の作業を実行します。 通常、ファイルシステムフィルタードライバーは、1つのコントロールデバイスオブジェクトと1つまたは複数のフィルターデバイスオブジェクトを作成します。

- **その他の相違点**

  - ファイルシステムフィルタードライバーはデバイスドライバーではないため、[ダイレクトメモリアクセス (DMA)](https://docs.microsoft.com/windows-hardware/drivers/kernel/using-direct-i-o-with-dma)は実行されません。

  - デバイスフィルタードライバーは、ターゲットデバイスの関数ドライバーの上または下にアタッチできますが、ファイルシステムフィルタードライバーは、ターゲットファイルシステムドライバーの上にしかアタッチできません。 したがって、デバイスドライバーの用語では、ファイルシステムフィルタードライバーは上位フィルターに限らず、フィルターを下げることはできません。
