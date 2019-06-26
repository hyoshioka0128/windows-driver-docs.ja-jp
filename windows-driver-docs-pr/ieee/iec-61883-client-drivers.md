---
title: IEC-61883 クライアント ドライバー
description: IEC-61883 クライアント ドライバー
ms.assetid: 2a3f62d0-c1f2-4978-8f89-3ed800d697f4
keywords:
- IEC 61883 クライアント ドライバー WDK IEEE 1394 バス
- 61883 WDK IEEE 1394 バス
- IEEE 1394 WDK バス、IEC 61883 クライアント ドライバー
- 1394 WDK バス、IEC 61883 クライアント ドライバー
- WDK のバスのプロトコル
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d29e9bbde632b70f9a3ba140c30747d0dc63f0cf
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385783"
---
# <a name="iec-61883-client-drivers"></a>IEC-61883 クライアント ドライバー





IEC 61883 は、IEEE 1394 オーディオおよびビデオのデバイスで使用される標準の通信とコントロールのインターフェイスです。 Windows 98 SE、Windows 2000 以前のオペレーティング システムで 61883 機能は、Microsoft デジタル ビデオ (MSDV) カムコーダー ドライバーの一部として実装されました*msdv.sys*します。 Windows Me、Windows XP、および以降のオペレーティング システムでは、61883 機能が 61883 をサポートする専用の個別のドライバーに移動されています。 IEC 61883 クライアント ドライバーのベンダーから提供された、システムが提供する要求を送信する[IEC 61883 プロトコル ドライバー](https://docs.microsoft.com/windows-hardware/drivers/ieee/iec-61883-protocol-driver) (*61883.sys*) 自分のデバイスと通信します。

IEC 61883 仕様では、どの多数のコンシューマーが電子的なオーディオおよびビデオ機器相互接続できますプロトコルを定義します。 これらの仕様には、一般的なデータ形式、データ フロー、およびオーディオビジュアル情報の接続の構成の定義が含まれます。 IEC 61883 プロトコル ドライバーには、次の承認済み IEC 61883 仕様に準拠しているデバイスがサポートされています。

-   IEC-61883-1:全般的な情報

-   IEC-61883-2:SD VCR データ転送

-   IEC-61883-3:HD VCR データ転送

-   IEC-61883-4:MPEG2 TS データ転送

-   IEC-61883-5:SDL DVCR データ転送

-   IEC-61883 6:オーディオおよび音楽データ伝送プロトコル

このセクションの内容:

[IEC 61883 プロトコル ドライバー](https://docs.microsoft.com/windows-hardware/drivers/ieee/iec-61883-protocol-driver)
[クライアント ドライバー スタックで IEC 61883 プロトコル ドライバー](https://docs.microsoft.com/windows-hardware/drivers/ieee/iec-61883-protocol-driver-in-a-client-driver-stack)
 

 




