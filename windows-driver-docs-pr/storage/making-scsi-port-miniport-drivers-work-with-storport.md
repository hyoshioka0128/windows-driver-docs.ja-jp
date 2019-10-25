---
title: SCSI ポート ミニポート ドライバーを Storport で動作させる
description: SCSI ポート ミニポート ドライバーを Storport で動作させる
ms.assetid: d2e8daaf-47e2-4a6c-9992-517dc107d4bd
keywords:
- Storport ドライバー WDK、SCSI ポートミニポートドライバー
- SCSI ポートドライバー WDK 記憶域、Storport ドライバー
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 910144a89d5d26a59cf0fa0e97eaa2cd2f75671b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841615"
---
# <a name="making-scsi-port-miniport-drivers-work-with-storport"></a>SCSI ポート ミニポート ドライバーを Storport で動作させる


## <span id="ddk_making_scsi_port_miniport_drivers_work_with_storport_kg"></span><span id="DDK_MAKING_SCSI_PORT_MINIPORT_DRIVERS_WORK_WITH_STORPORT_KG"></span>


Storport ミニポートドライバーのインターフェイスは、scsi ポートミニポートドライバーを使用して Storport ドライバーを操作できるようにするために、SCSI ポートミニポートドライバーのインターフェイスと同様に設計されています。 SCSI ポートミニポートドライバーが Storport で動作するようにするには、次の基本的な手順を実行する必要があります。

1.  \#のすべてのインスタンスを変更し*ます。* これには、&lt;の&gt; ディレクティブ**が**含まれます。このディレクティブには、\#が &lt;**含ま***れてい*ます。

    *Scsi .h*ファイルと*storport*ヘッダーファイルの両方が含まれている場合は、コンパイル時エラーが発生します。

2.  ビルドスクリプト内の csiport を*使用して、* ソースファイルまたは**メイク**ファイルファイルで sを置き換えます。

3.  すべての展開された構造体が適切に初期化されていることを確認します。

    [**ハードウェア\_初期化\_データ (scsi)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_hw_initialization_data)構造と[**ポート\_CONFIGURATION\_情報 (scsi)** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information)構造の両方のサイズが変更されたため、新しいメンバーが正しく初期化されていることを確認してください。

Storport ヘッダーファイル*storport で*は、scsi ポートからの移植を容易にするために、scsi ポートプレフィックス付きコマンドと storport プレフィックス付きコマンドの両方が現在保持されています。

このセクションでは、ドライバー作成者向けに、SCSI ポートで動作するように設計されたミニポートドライバーを変更する手順について詳しく説明します。これにより、Storport で使用できるようになります。 次のトピックについて説明します。

[Storport をアダプターと共に使用するための要件](requirements-for-using-storport-with-an-adapter.md)

[Storport を使用したハードウェアの初期化](hardware-initialization-with-storport.md)

[Storport を使用したポート構成情報の設定](setting-port-configuration-information-with-storport.md)

 

 




